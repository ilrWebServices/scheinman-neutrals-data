# Scheinman Neutrals Data for Migration

This data was generated from the D7 site via the following queries:

```sql
select 
  u.uid, u.name, u.pass, u.mail, u.created, u.access, u.login, u.timezone, u.init, u.changed
from users u
where u.uid in (
  select distinct uid from node where type = 'scheinman_neutral'
);
```

```sql
select n.nid, n.vid, n.uid, n.title, n.created as n_created, n.changed as n_changed,
  fname.field_first_name_value as fname,
  lname.field_last_name_value as lname,
  mname.field_middle_name_value as mname,
  namet.field_name_title_value as name_title,
  namesuf.field_suffix_value as name_suffix,
  c.field_company_value as company,
  fm.field_email_email as email,
  fjt.field_job_title_value as job_title,
  fp.field_phone_value as phone,
  ff.field_fax_value as fax,
  addy1.field_address_line_1_value as addr_1,
  addy2.field_address_line_2_value as addr_2,
  city.field_city_value as city,
  st.field_state_inc_outside_us_value as state,
  zip.field_zip_code_value as zip,
  group_concat(fw.field_website_url_url separator ';') as websites,
  fwh.field_professional_work_history__value as prof_work_history,
  fdre.field_dispute_resolution_experie_value as dispute_resolution_experience,
  fdrt.field_dispute_resolution_trainin_value as dispute_resolution_training,
  fdra.field_additional_dispute_resolut_value as dispute_resolution_additional,
  fpa.field_professional_associations_value as professional_associations,
  fe.field_education_value as education,
  fr.field_references_value as `references`,
  ffp.field_fee_policy_value as fee_policy,
  replace(file_image.uri, "public://", "https://www.ilr.cornell.edu/sites/default/files/") as image_uri
from node n
left join field_data_field_email fm on n.nid = fm.entity_id and n.vid = fm.revision_id

left join field_data_field_first_name fname on n.nid = fname.entity_id and n.vid = fname.revision_id
left join field_data_field_last_name lname on n.nid = lname.entity_id and n.vid = lname.revision_id
left join field_data_field_middle_name mname on n.nid = mname.entity_id and n.vid = mname.revision_id
left join field_data_field_name_title namet on n.nid = namet.entity_id and n.vid = namet.revision_id
left join field_data_field_suffix namesuf on n.nid = namesuf.entity_id and n.vid = namesuf.revision_id
left join field_data_field_company c on n.nid = c.entity_id and n.vid = c.revision_id

left join field_data_field_address_line_1 addy1 on n.nid = addy1.entity_id and n.vid = addy1.revision_id
left join field_data_field_address_line_2 addy2 on n.nid = addy2.entity_id and n.vid = addy2.revision_id
left join field_data_field_city city on n.nid = city.entity_id and n.vid = city.revision_id
left join field_data_field_state_inc_outside_us st on n.nid = st.entity_id and n.vid = st.revision_id
left join field_data_field_zip_code zip on n.nid = zip.entity_id and n.vid = zip.revision_id

left join field_data_field_job_title fjt on n.nid = fjt.entity_id and n.vid = fjt.revision_id
left join field_data_field_phone fp on n.nid = fp.entity_id and n.vid = fp.revision_id
left join field_data_field_fax ff on n.nid = ff.entity_id and n.vid = ff.revision_id
left join field_data_field_website_url fw on n.nid = fw.entity_id and n.vid = fw.revision_id
left join field_data_field_professional_work_history_ fwh on n.nid = fwh.entity_id and n.vid = fwh.revision_id
left join field_data_field_dispute_resolution_experie fdre on n.nid = fdre.entity_id and n.vid = fdre.revision_id
left join field_data_field_dispute_resolution_trainin fdrt on n.nid = fdrt.entity_id and n.vid = fdrt.revision_id
left join field_data_field_additional_dispute_resolut fdra on n.nid = fdra.entity_id and n.vid = fdra.revision_id
left join field_data_field_professional_associations fpa on n.nid = fpa.entity_id and n.vid = fpa.revision_id
left join field_data_field_education fe on n.nid = fe.entity_id and n.vid = fe.revision_id
left join field_data_field_references fr on n.nid = fr.entity_id and n.vid = fr.revision_id
left join field_data_field_fee_policy ffp on n.nid = ffp.entity_id and n.vid = ffp.revision_id
left join field_data_field_profile_image fi on n.nid = fi.entity_id and n.vid = fi.revision_id
left join file_managed file_image on fi.field_profile_image_fid = file_image.fid
where n.type = 'scheinman_neutral'
  and n.status = 1
group by n.nid
order by n.title;
```
