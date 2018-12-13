## Baltimore Area

### Baltimore City

#### Downtown Baltimore
```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '245100401001' or
	od.w_bgrp = '245100401002' or
	od.w_bgrp = '245100604001' or
	od.w_bgrp = '245100402001' or
	od.w_bgrp = '245100704002' or
	od.w_bgrp = '245100302002' or
	od.w_bgrp = '245100203002' or
	od.w_bgrp = '245101702003' or
	od.w_bgrp = '245102101001' or
	od.w_bgrp = '245102401001' or
	od.w_bgrp = '245101102001' or
	od.w_bgrp = '245102201001' or
	od.w_bgrp = '245102201003' or
	od.w_bgrp = '245102805002' or
	od.w_bgrp = '245101003001' or
	od.w_bgrp = '245101102002' or
	od.w_bgrp = '245100604002' or
	od.w_bgrp = '245101701001' or
	od.w_bgrp = '245102201002' or
	od.w_bgrp = '245101101002' or
	od.w_bgrp = '245102402001' or
	od.w_bgrp = '245101702001' or
	od.w_bgrp = '245101401001' or
	od.w_bgrp = '245100302001' or
	od.w_bgrp = '245100203003'
group by "bgrp" order by "workers" desc
```

#### Pikesville-Fallstaff

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '245102801021' or
	od.w_bgrp = '245102801012' or
	od.w_bgrp = '240054034022' or
	od.w_bgrp = '240054034021' or
	od.w_bgrp = '240054034012' or
	od.w_bgrp = '240054037011' or
	od.w_bgrp = '240054034011'
group by "bgrp" order by "workers" desc
```

#### Hamden-Charles Village

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '245101202021' or
	od.w_bgrp = '245101207001' or
	od.w_bgrp = '245101202022' or
	od.w_bgrp = '245101308061' or
	od.w_bgrp = '245101307001' or
	od.w_bgrp = '245102711021' or
	od.w_bgrp = '245101206002' or
	od.w_bgrp = '245101207003' or
	od.w_bgrp = '245101308042' or
	od.w_bgrp = '245101206003' or
	od.w_bgrp = '245100905002'
group by "bgrp" order by "workers" desc
```

### Baltimore Suburbs

#### Lutherville-Timonium

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240054084001' or
	od.w_bgrp = '240054081002' or
	od.w_bgrp = '240054085052' or
	od.w_bgrp = '240054088001' or
	od.w_bgrp = '240054088002' or
	od.w_bgrp = '240054902002' or
	od.w_bgrp = '240054087042' or
	od.w_bgrp = '240054085031' or
	od.w_bgrp = '240054085032'
group by "bgrp" order by "workers" desc
```

#### Columbia

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240276054023' or
	od.w_bgrp = '240276056021' or
	od.w_bgrp = '240276054021' or
	od.w_bgrp = '240276054024' or
	od.w_bgrp = '240276067071' or
	od.w_bgrp = '240276067061' or
	od.w_bgrp = '240276067072' or
	od.w_bgrp = '240276067051' or
	od.w_bgrp = '240276067011'
group by "bgrp" order by "workers" desc
```

#### Towson

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240054907031' or
	od.w_bgrp = '240054906051' or
	od.w_bgrp = '240054909002' or
	od.w_bgrp = '240054906052' or
	od.w_bgrp = '240054909001' or
	od.w_bgrp = '240054907011' or
	od.w_bgrp = '240054903012' or
	od.w_bgrp = '240054912011' or
	od.w_bgrp = '240054903022' or
	od.w_bgrp = '240054912012' or
	od.w_bgrp = '240054909003' or
	od.w_bgrp = '240054903013' or
	od.w_bgrp = '240054903011'
group by "bgrp" order by "workers" desc
```

#### White Marsh-Rossville

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240054407012' or
	od.w_bgrp = '240054113072' or
	od.w_bgrp = '240054512001' or
	od.w_bgrp = '240054406001' or
	od.w_bgrp = '240054407021' or
	od.w_bgrp = '240054517012' or
	od.w_bgrp = '240054407022' or
	od.w_bgrp = '240054408001'
group by "bgrp" order by "workers" desc
```

#### South Baltimore County

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240054304003' or
	od.w_bgrp = '240054001002' or
	od.w_bgrp = '240054925001' or
	od.w_bgrp = '240054010001' or
	od.w_bgrp = '245102501031' or
	od.w_bgrp = '240054004002' or
	od.w_bgrp = '245102501032' or
	od.w_bgrp = '240054304001' or
	od.w_bgrp = '240054304002'
group by "bgrp" order by "workers" desc
```

## Washington area

### District of Columbia

#### Old Downtown DC

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '110010052014' or
	od.w_bgrp = '110010047012' or
	od.w_bgrp = '110010050022' or
	od.w_bgrp = '110010083012' or
	od.w_bgrp = '110010052012' or
	od.w_bgrp = '110010049012' or
	od.w_bgrp = '110010049022' or
	od.w_bgrp = '110010048011' or
	od.w_bgrp = '110010047021' or
	od.w_bgrp = '110010059001' or
	od.w_bgrp = '110010058002' or
	od.w_bgrp = '110010101002' or
	od.w_bgrp = '110010101001' or
	od.w_bgrp = '110010106002' or
	od.w_bgrp = '110010058001' or
	od.w_bgrp = '110010062021'
	group by "bgrp" order by "workers" desc
```

#### New Downtown DC

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '110010042022' or
	od.w_bgrp = '110010053012' or
	od.w_bgrp = '110010055005' or
	od.w_bgrp = '110010042021' or
	od.w_bgrp = '110010056004' or
	od.w_bgrp = '110010055004' or
	od.w_bgrp = '110010056002' or
	od.w_bgrp = '110010053013' or
	od.w_bgrp = '110010055001' or
	od.w_bgrp = '110010055002' or
	od.w_bgrp = '110010108001' or
	od.w_bgrp = '110010055003' or
	od.w_bgrp = '110010108002' or
	od.w_bgrp = '110010107002' or
	od.w_bgrp = '110010107001'
	group by "bgrp" order by "workers" desc
```

#### L'Enfant Plaza-Capitol Hill

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '110010065002' or
	od.w_bgrp = '110010065001' or
	od.w_bgrp = '110010066001' or
	od.w_bgrp = '110010070002' or
	od.w_bgrp = '110010105002' or
	od.w_bgrp = '110010067003' or
	od.w_bgrp = '110010072002' or
	od.w_bgrp = '110010102001' or
	od.w_bgrp = '110010102002'
	group by "bgrp" order by "workers" desc
```

#### Georgetown

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '110010002011' or
	od.w_bgrp = '110010001004' or
	od.w_bgrp = '110010002024' or
	od.w_bgrp = '110010002023'
	group by "bgrp" order by "workers" desc
```

### Maryland Suburbs

#### Gaithersburg

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240317008173' or
	od.w_bgrp = '240317010072' or
	od.w_bgrp = '240317008171' or
	od.w_bgrp = '240317007182' or
	od.w_bgrp = '240317007181' or
	od.w_bgrp = '240317008291' or
	od.w_bgrp = '240317010071' or
	od.w_bgrp = '240317007231' or
	od.w_bgrp = '240317007191' or
	od.w_bgrp = '240317012113' or
	od.w_bgrp = '240317007221' or
	od.w_bgrp = '240317007173' or
	od.w_bgrp = '240317007132' or
	od.w_bgrp = '240317007042' or
	od.w_bgrp = '240317007061' or
	od.w_bgrp = '240317007222' or
	od.w_bgrp = '240317008221' or
	od.w_bgrp = '240317012212' or
	od.w_bgrp = '240317008163' or
	od.w_bgrp = '240317008261' or
	od.w_bgrp = '240317012112' or
	od.w_bgrp = '240317008241'
	group by "bgrp" order by "workers" desc
```

#### Rockville Pike

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240317009012' or
	od.w_bgrp = '240317009011' or
	od.w_bgrp = '240317012191' or
	od.w_bgrp = '240317009041' or
	od.w_bgrp = '240317012163' or
	od.w_bgrp = '240317012162' or
	od.w_bgrp = '240317012135' or
	od.w_bgrp = '240317012183' or
	od.w_bgrp = '240317012181' or
	od.w_bgrp = '240317010013' or
	od.w_bgrp = '240317012021' or
	od.w_bgrp = '240317009052' or
	od.w_bgrp = '240317009042'
	group by "bgrp" order by "workers" desc
```

#### Bethesda

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240317048052' or
	od.w_bgrp = '240317050001' or
	od.w_bgrp = '240317046001' or
	od.w_bgrp = '240317048061' or
	od.w_bgrp = '240317048033' or
	od.w_bgrp = '240317048031' or
	od.w_bgrp = '240317048062' or
	od.w_bgrp = '240317048051' or
	od.w_bgrp = '240317048041' or
	od.w_bgrp = '240317050004'
	group by "bgrp" order by "workers" desc
```

#### College Park-Hyattsville

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240338070002' or
	od.w_bgrp = '240338071022' or
	od.w_bgrp = '240338072004' or
	od.w_bgrp = '240338063001' or
	od.w_bgrp = '240338065011' or
	od.w_bgrp = '240338059082' or
	od.w_bgrp = '240338072002'
	group by "bgrp" order by "workers" desc
```

#### Silver Spring

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240317025004' or
	od.w_bgrp = '240317028002' or
	od.w_bgrp = '240317025001' or
	od.w_bgrp = '240317026012' or
	od.w_bgrp = '110010016002' or
	od.w_bgrp = '110010017022' or
	od.w_bgrp = '110010016001'
	group by "bgrp" order by "workers" desc
```

### Northern Virginia Suburbs

#### Tysons

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '510594609001' or
	od.w_bgrp = '510594610001' or
	od.w_bgrp = '510594608002' or
	od.w_bgrp = '510594605023' or
	od.w_bgrp = '510594706002' or
	od.w_bgrp = '510594607021' or
	od.w_bgrp = '510594711001' or
	od.w_bgrp = '510594707001' or
	od.w_bgrp = '510594712021' or
	od.w_bgrp = '510594713011' or
	od.w_bgrp = '510594608001' or
	od.w_bgrp = '510594712012' or
	od.w_bgrp = '510594712011' or
	od.w_bgrp = '510594705004' or
	od.w_bgrp = '510594712023' or
	od.w_bgrp = '510594605011' or
	od.w_bgrp = '510594604003' or
	od.w_bgrp = '510594712022' or
	od.w_bgrp = '510594802021' or
	od.w_bgrp = '510594802031' or
	od.w_bgrp = '510594802022'
	group by "bgrp" order by "workers" desc
```

#### Reston

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '510594812011' or
	od.w_bgrp = '510594808021' or
	od.w_bgrp = '510594825015' or
	od.w_bgrp = '510594808012' or
	od.w_bgrp = '510594808022' or
	od.w_bgrp = '510594822031' or
	od.w_bgrp = '510594809032' or
	od.w_bgrp = '510594825012' or
	od.w_bgrp = '510594823011' or
	od.w_bgrp = '510594822032' or
	od.w_bgrp = '510594811011' or
	od.w_bgrp = '510594824001' or
	od.w_bgrp = '510594809021' or
	od.w_bgrp = '510594819002' or
	od.w_bgrp = '510594812023' or
	od.w_bgrp = '510594822022' or
	od.w_bgrp = '510594825013' or
	od.w_bgrp = '510594822034'
	group by "bgrp" order by "workers" desc
```

#### Fair Oaks

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '510594917032' or
	od.w_bgrp = '510594917022' or
	od.w_bgrp = '510594405021' or
	od.w_bgrp = '510594917011' or
	od.w_bgrp = '510594612021' or
	od.w_bgrp = '510594826023' or
	od.w_bgrp = '510594612022' or
	od.w_bgrp = '516003002003' or
	od.w_bgrp = '510594405023' or
	od.w_bgrp = '510594917031' or
	od.w_bgrp = '510594918011' or
	od.w_bgrp = '510594618023' or
	od.w_bgrp = '516003001003' or
	od.w_bgrp = '516003004002' or
	od.w_bgrp = '510594817022' or
	od.w_bgrp = '516003005003' or
	od.w_bgrp = '516003002004' or
	od.w_bgrp = '510594917042' or
	od.w_bgrp = '510594917012' or
	od.w_bgrp = '516003001002' or
	od.w_bgrp = '516003004001' or
	od.w_bgrp = '510594618021' or
	od.w_bgrp = '510594917021' or
	od.w_bgrp = '516003002002' or
	od.w_bgrp = '510594918021'
	group by "bgrp" order by "workers" desc
```

#### Rosslyn-Ballston Corridor

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '510131016033' or
	od.w_bgrp = '510131018011' or
	od.w_bgrp = '510131018021' or
	od.w_bgrp = '510131014031' or
	od.w_bgrp = '510131014011' or
	od.w_bgrp = '510131014021' or
	od.w_bgrp = '510131017022' or
	od.w_bgrp = '510131015003' or
	od.w_bgrp = '510131014032' or
	od.w_bgrp = '510131014022' or
	od.w_bgrp = '510131016022' or
	od.w_bgrp = '510131014041' or
	od.w_bgrp = '510131017013' or
	od.w_bgrp = '510131014034' or
	od.w_bgrp = '510131016032' or
	od.w_bgrp = '510131015004' or
	od.w_bgrp = '510131017014' or
	od.w_bgrp = '510131019001' or
	od.w_bgrp = '510131014033' or
	od.w_bgrp = '510131020032'
	group by "bgrp" order by "workers" desc
```

#### East Alexandria

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '515102018013' or
	od.w_bgrp = '515102019002' or
	od.w_bgrp = '515102007021' or
	od.w_bgrp = '515102019001' or
	od.w_bgrp = '515102018014' or
	od.w_bgrp = '515102018012' or
	od.w_bgrp = '515102018022' or
	od.w_bgrp = '515102016002'
	group by "bgrp" order by "workers" desc
```

#### South Arlington

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '510131034021' or
	od.w_bgrp = '510131035021' or
	od.w_bgrp = '510131034024' or
	od.w_bgrp = '510131034023' or
	od.w_bgrp = '510139802001' or
	od.w_bgrp = '510131034022' or
	od.w_bgrp = '510131035032' or
	od.w_bgrp = '510131034025'
	group by "bgrp" order by "workers" desc
```

## Small Cities

### Annapolis

```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240037063012' or
	od.w_bgrp = '240037066005' or
	od.w_bgrp = '240037065001' or
	od.w_bgrp = '240037025001' or
	od.w_bgrp = '240037065002' or
	od.w_bgrp = '240037063023' or
	od.w_bgrp = '240037066002' or
	od.w_bgrp = '240037061011' or
	od.w_bgrp = '240037065004' or
	od.w_bgrp = '240037024021' or
	od.w_bgrp = '240037066003' or
	od.w_bgrp = '240037061012' or
	od.w_bgrp = '240037027011' or
	od.w_bgrp = '240037024022'
group by "bgrp" order by "workers" desc
```

### Frederick
```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240217508012' or
	od.w_bgrp = '240217651001' or
	od.w_bgrp = '240217506001' or
	od.w_bgrp = '240217508031' or
	od.w_bgrp = '240217506003' or
	od.w_bgrp = '240217722001' or
	od.w_bgrp = '240217512012' or
	od.w_bgrp = '240217508023' or
	od.w_bgrp = '240217502001' or
	od.w_bgrp = '240217512011' or
	od.w_bgrp = '240217523012' or
	od.w_bgrp = '240217507012' or
	od.w_bgrp = '240217722002' or
	od.w_bgrp = '240217502002' or
	od.w_bgrp = '240217510031' or
	od.w_bgrp = '240217510033'
group by "bgrp" order by "workers" desc
```

### Hagerstown
```sql
select
	od.h_bgrp as "bgrp",
	ifnull(sum(od.workers),0) as "workers"
from od_bg_data as od
where
	od.w_bgrp = '240430103001' or
	od.w_bgrp = '240430103001' or
	od.w_bgrp = '240430105004' or
	od.w_bgrp = '240430009002' or
	od.w_bgrp = '240430009003' or
	od.w_bgrp = '240430112013' or
	od.w_bgrp = '240430006022' or
	od.w_bgrp = '240430010011' or
	od.w_bgrp = '240430006011' or
	od.w_bgrp = '240430004003' or
	od.w_bgrp = '240430103003' or
	od.w_bgrp = '240430006021' or
	od.w_bgrp = '240430111003' or
	od.w_bgrp = '240430002002' or
	od.w_bgrp = '240430003011' or
	od.w_bgrp = '240430005001' or
group by "bgrp" order by "workers" desc
```
