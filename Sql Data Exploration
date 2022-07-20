select*from myportfolio.dbo.CovidDeaths

select *from myportfolio..CovidDeaths
order by 3,4


select *from myportfolio..CovidVaccinations
order by 3,4


select location,date,total_cases,new_cases,total_deaths,population from myportfolio..CovidDeaths
order by 1,2

select location,date,total_cases,new_cases,total_deaths,(total_deaths/total_cases)*100 as deathpercentage  
from  myportfolio..CovidDeaths
order by 1,2

select location,date,total_cases,new_cases,total_deaths,(total_deaths/total_cases)*100 as deathpercentage  
from  myportfolio..CovidDeaths
order by 1,2 desc

select location,date,total_cases,new_cases,total_deaths,(total_deaths/total_cases)*100 as deathpercentage  
from  myportfolio..CovidDeaths
where location like 'india'
order by 1,2 desc


select location,date,total_cases,new_cases,total_deaths,(total_deaths/total_cases)*100 as deathpercentage  
from  myportfolio..CovidDeaths
where location like '%state%'
order by 1,2



-- Shows what percentage of population got Covid
Select Location,date,Population,total_cases,(total_cases/population)*100 as populationinfectedcovid
From   myportfolio..CovidDeaths
Where location like'%states%'
              

--looking at contries which is highest infected rate with population
Select Location,Population,max(total_cases) as highestinfectedcount,max((total_cases/population))*100 as populationinfectedcovid
From   myportfolio..CovidDeaths
group by Location,Population
order by populationinfectedcovid desc

Select Location,max(cast(total_deaths as int)) as deathcount,max((total_deaths/population))*100 as totaldeathcount
From   myportfolio..CovidDeaths
where continent is not null
group by Location
order by totaldeathcount desc

Select continent,max(cast(total_deaths as int)) as deathcount,max((total_deaths/population))*100 as totaldeathcount
From   myportfolio..CovidDeaths
where continent is not null
group by continent
order by totaldeathcount desc

--looking at total population and vacsinated

select*from myportfolio..CovidDeaths dea
join myportfolio..CovidVaccinations vac
on dea.location=vac.location
and dea.date=vac.date

drop table if exists #percentpopulationvaccinated
create table #percentpopulationvaccinated
(
continent nvarchar(255),
location nvarchar(255),
date datetime,
population numeric,
new_vaccinations numeric,
rollingpeoplevaccinated numeric
)


insert into #percentpopulationvaccinated
select dea.continent,dea.location, dea.date,dea.population,vac.new_vaccinations,
sum(convert(int,vac.new_vaccinations)) over (partition by dea.location order by dea.location,dea.date) as rollingpeoplevaccinated
from myportfolio..CovidDeaths dea
join myportfolio..CovidVaccinations vac
on dea.location=vac.location
and dea.date=vac.date
--where dea.continent is not null
--order by 1,2 ,3



select*,(rollingpeoplevaccinated/population)*100
from percentpopulationvaccinated


--creating view to store data for later visulization

create view percentpopulationvaccinateds as
select dea.continent,dea.location, dea.date,dea.population,vac.new_vaccinations,
sum(convert(int,vac.new_vaccinations)) over (partition by dea.location order by dea.location,dea.date) as rollingpeoplevaccinated
from myportfolio..CovidDeaths dea
join myportfolio..CovidVaccinations vac
on dea.location=vac.location
and dea.date=vac.date
where dea.continent is not null
--order by 1,2 ,3

select * from percentpopulationvaccinateds
