# workonhive
save the codes
create table joined
(
vd string,
store string,
no_of_stores bigint,
total_revenue bigint,
no_of_visit bigint
)
row format delimited fields terminated by ','
stored as textfile
select a.visit, a.store, a.no_of_stores, a.total_revenue, b.no_of_visit
from store_sales a join store_visit b
on (a.store = b.store);

create table joined as
select a.visit, a.store, a.no_of_stores, a.total_revenue, b.no_of_visit
from store_sales a join store_visit b
on (a.store = b.store);

description store_visit;

select * 
from joined
limit 5;

alter table joined
add partition (visit_date)
location '/home/saurabh.gupta/store';

select store, count(store)  
from joined
group by store
having count(store)>400;
order by store;
