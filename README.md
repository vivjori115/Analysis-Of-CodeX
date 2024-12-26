# Analysis-Of-CodeX--RC6
CodeX is a German beverage company that is aiming to make its mark in the Indian market. A few months ago, they launched their energy drink in 10 cities in India.
Their Marketing team is responsible for increasing brand awareness, market share, and product development. They conducted a survey in those 10 cities and received results from 10k respondents.

### overall Consumers are 10K. Out of Total Consumers There Are total 980 consumers of CodeX which was 10% of overall consumers .

```sql
use sql_project;
select * from dim_cities;
select * from dim_repondents;
select * from fact_survey_responses;
```

```sql
select count(respondent_id) from fact_survey_responses
select count(respondent_id),current_brands from fact_survey_responses
group by current_brands
```

## -- Who prefers energy drink more? (male/female/non-binary?)
```sql
select count(r.respondent_id) as no_of_respondent,gender from dim_repondents r
join fact_survey_responses s on r.respondent_id=s.respondent_id
group by gender
order by no_of_respondent desc
```

## -- Which age group prefers energy drinks more?
```sql
select count(r.respondent_id) as no_of_respondent,age from dim_repondents r
join fact_survey_responses s on r.respondent_id=s.respondent_id
where current_brands = "CodeX"
group by age
order by no_of_respondent desc
```

## -- Which type of marketing reaches the most Youth (15-30)?
```sql
select age,marketing_channels,count(r.respondent_id) as coun from dim_repondents r
join fact_survey_responses s on r.respondent_id=s.respondent_id
group by age,marketing_channels
order by coun desc
```

## -- What are the preferred ingredients of energy drinks among respondents?
```sql
select Ingredients_expected,count(respondent_id) as coun from fact_survey_responses
group by Ingredients_expected
order by coun desc
```

## -- What packaging preferences do respondents have for energy drinks?
```sql
select Packaging_preference,count(respondent_id) as coun from fact_survey_responses
group by Packaging_preference
order by coun desc
```

## -- Who are the current market leaders?
```sql
select count(respondent_id) as coun,current_brands from fact_survey_responses
group by current_brands 
order by coun desc
```

## -- What are the primary reasons consumers prefer those brands over ours?
```sql
select distinct(Consume_reason) from fact_survey_responses
select count(respondent_id) as coun,Consume_reason from fact_survey_responses
where current_brands !="CodeX"
group by Consume_reason 
order by coun desc
```

## -- Which marketing channel can be used to reach more customers?
```sql
select marketing_channels,count(r.respondent_id) as coun from dim_repondents r
join fact_survey_responses s on r.respondent_id=s.respondent_id
where current_brands = "CodeX"
group by marketing_channels
order by coun desc
```

## -- How effective are different marketing strategies and channels in reaching our customers?
```sql
select marketing_channels,count(r.respondent_id) as coun from dim_repondents r
join fact_survey_responses s on r.respondent_id=s.respondent_id
group by marketing_channels
order by coun desc
```

## -- What do people think about our brand? (overall rating)
```sql
select current_brands,sum(taste_experience) as su from fact_survey_responses 
group by current_brands
order by su desc
having current_brands = "CodeX"
```

```sql
select count(respondent_id) as coun from fact_survey_responses 
where taste_experience = 5 and current_brands = "CodeX" 
```

```sql
select city,count(r.respondent_id) as coun,current_brands from dim_cities c 
join dim_repondents r on r.city_id=c.city_id
join fact_survey_responses f on r.respondent_id=f.respondent_id
where current_brands = "CodeX"
group by city
order by coun desc
```

## -- Where do respondents prefer to purchase energy drinks?
```sql
select count(respondent_id) as coun ,purchase_location from fact_survey_responses
group by purchase_location
order by coun desc
```

## -- What are the typical consumption situations for energy drinks among respondents?
```sql
select count(respondent_id) as coun,typical_consumption_situations from fact_survey_responses
where current_brands = "CodeX"
group by typical_consumption_situations 
order by coun desc
```

## -- What factors influence respondents' purchase decisions, such as price range and limited edition packaging?
```sql
select price_range,limited_edition_packaging,count(respondent_id) as coun from fact_survey_responses
group by price_range,limited_edition_packaging
order by coun desc
```

## -- Which area of business should we focus more on our product development? (Branding/taste/availability)
```sql
select reasons_for_choosing_brands,count(respondent_id) as coun ,current_brands from fact_survey_responses
group by reasons_for_choosing_brands,current_brands
having current_brands = "CodeX"
order by coun desc
```

## -- What immediate improvements can we bring to the product?
```sql
select count(respondent_id) as coun,Improvements_desired,current_brands from fact_survey_responses
group by improvements_desired,current_brands
having current_brands = "CodeX"
order by coun desc
```

## -- What should be the ideal price of our product?
```sql
select current_brands,price_range,count(respondent_id) as coun from fact_survey_responses
where current_brands = "Codex"
group by  current_brands,price_range
```

## -- What kind of marketing campaigns, offers, and discounts we can run?
```sql
select marketing_channels,count(r.respondent_id) as coun from dim_repondents r
join fact_survey_responses s on r.respondent_id=s.respondent_id
group by marketing_channels
order by coun desc
```

```sql
select Consume_frequency,count(respondent_id) as coun from fact_survey_responses
group by Consume_frequency
order by coun desc
```

```sql
select Consume_frequency,count(respondent_id) as coun from fact_survey_responses
where current_brands = "CodeX" 
group by Consume_frequency
order by coun desc
```

```sql
select Heard_before,count(respondent_id) as coun from fact_survey_responses
where current_brands="CodeX"
group by Heard_before
order by coun desc
```

```sql
select Brand_perception,count(respondent_id) as coun from fact_survey_responses
where current_brands="CodeX"
group by Brand_perception
order by coun desc
```

```sql
select General_perception,count(respondent_id) as coun from fact_survey_responses
where current_brands="CodeX"
group by General_perception
order by coun desc
```