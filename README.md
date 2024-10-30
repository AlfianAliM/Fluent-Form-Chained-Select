with kota as (
    select 
        "Kode",
        "Nama",
        case 
            when "Kode" like '%00' then 'provinsi'
            else 'wilayah' 
        end as "wilayah"
    from "Data Analyst".kotaprovinsi
    where length("Kode") = 5
)
select 
    case 
        when a."wilayah" = 'provinsi' then a."Nama"
        else b."Nama"
    end as provinsi,
    case 
        when a."wilayah" = 'wilayah' then a."Nama"
        else null
    end as nama_kota
from kota a
left join kota b on left(a."Kode", 2) = left(b."Kode", 2) and b."wilayah" = 'provinsi'
where a."wilayah" = 'wilayah'
order by a."Kode"




