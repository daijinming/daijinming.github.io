- 选择第一条记录  
select * from (select * from personnum_cameral_history order by id desc ) where rownum<=1 order by rownum asc
