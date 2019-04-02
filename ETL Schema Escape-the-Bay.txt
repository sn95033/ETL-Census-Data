-- Exported from QuickDBD: https://www.quickdatatabasediagrams.com/
-- Link to schema: https://app.quickdatabasediagrams.com/#/d/S3gYBf
-- NOTE! If you have used non-SQL datatypes in your design, you will have to change these here.

-- To reset the sample schema, replace everything with
-- two dots ('..' - without quotes).

CREATE TABLE "destinations" (
    "index" INTEGER   NOT NULL,
    "state_county_fips" VARCHAR(255)   NOT NULL,
    "state_fips" VARCHAR(255)   NOT NULL,
    "county_fips" VARCHAR(255)   NOT NULL,
    "county_name" VARCHAR(255)   NOT NULL,
    "state_name" VARCHAR(255)   NOT NULL,
    "number_migrated_2017" INTEGER   NOT NULL,
    "margin_of_error" INTEGER   NOT NULL,
    CONSTRAINT "pk_destinations" PRIMARY KEY (
        "county_name"
     )
);

CREATE TABLE "demographics" (
    "county_name" VARCHAR(255)   NOT NULL,
    "population_estimate_2017" INTEGER   NOT NULL,
    "population_census_2010" INTEGER   NOT NULL,
    "age_under_5yrs_pct" FLOAT   NOT NULL,
    "age_under_18yrs_pct" FLOAT   NOT NULL,
    "age_above_65yrs_pct" FLOAT   NOT NULL,
    "median_home" INTEGER   NOT NULL,
    "med_monthly_cost_with_mortgage" INTEGER   NOT NULL,
    "med_monthly_cost_no_mortgage" INTEGER   NOT NULL,
    "median_monthly_rent" INTEGER   NOT NULL,
    "employment_pct" FLOAT   NOT NULL,
    "employment_females_pct" FLOAT   NOT NULL,
    "mean_travel_time_to_work" FLOAT   NOT NULL,
    "median_household_income" INT   NOT NULL,
    "number_of_employers_2016" INTEGER   NOT NULL,
    "total_employed_2016" INTEGER   NOT NULL,
    "annual_payroll_2016_1Kdollars" INTEGER   NOT NULL,
    "total_employment_pct_change_2015_2016" FLOAT   NOT NULL,
    "total_nonemployers" INTEGER   NOT NULL,
    "number_of_employers_2012" INTEGER   NOT NULL,
    "state_county_fips" INTEGER   NOT NULL,
    CONSTRAINT "pk_demographics" PRIMARY KEY (
        "state_county_fips"
     )
);

CREATE TABLE "financial" (
    "county_name" VARCHAR(255)   NOT NULL,
    "mortgages_valued_lt_50K_pct" FLOAT   NOT NULL,
    "mortgages_valued_50-99K_pct" FLOAT   NOT NULL,
    "mortgages_valued_100-299K_pct" FLOAT   NOT NULL,
    "mortgages_valued_300-499K_pct" FLOAT   NOT NULL,
    "mortgages_valued_500-749K_pct" FLOAT   NOT NULL,
    "mortgages_valued_750-999K_pct" FLOAT   NOT NULL,
    "mortgages_valued_gt_1M_pct" FLOAT   NOT NULL,
    "median_mortgage_value" INTEGER   NOT NULL,
    "household_income_lt_10K" FLOAT   NOT NULL,
    "household_income_10-24K" FLOAT   NOT NULL,
    "household_income_25-34K" FLOAT   NOT NULL,
    "household_income_35-49K_pct" FLOAT   NOT NULL,
    "household_income_50-74K_pct" FLOAT   NOT NULL,
    "household_income_75-99K_pct" FLOAT   NOT NULL,
    "household_income_100-150K_pct" FLOAT   NOT NULL,
    "household_income_gt_150K_pct" FLOAT   NOT NULL,
    "median_household_income_2017" INTEGER   NOT NULL,
    "mortgage_to_income_Ratio_lt_2" FLOAT   NOT NULL,
    "mortgage_to_income_Ratio_2-3" FLOAT   NOT NULL,
    "mortgage_to_income_Ratio_3-4.9" FLOAT   NOT NULL,
    "mortgage_to_income_Ratio_gt_4.0" FLOAT   NOT NULL,
    "state_county_fips" INTEGER   NOT NULL,
    CONSTRAINT "pk_financial" PRIMARY KEY (
        "state_county_fips"
     )
);

CREATE TABLE "home" (
    "county_name" VARCHAR(255)   NOT NULL,
    "state_fips" VARCHAR(255)   NOT NULL,
    "county_fips" VARCHAR(255)   NOT NULL,
    "med_home_value" INTEGER   NOT NULL,
    "med_rent" INTEGER   NOT NULL,
    "home_ownership_rate_pct" FLOAT   NOT NULL,
    CONSTRAINT "pk_home" PRIMARY KEY (
        "state_fips","county_fips"
     )
);

ALTER TABLE "demographics" ADD CONSTRAINT "fk_demographics_county_name" FOREIGN KEY("county_name")
REFERENCES "destinations" ("county_name");

ALTER TABLE "financial" ADD CONSTRAINT "fk_financial_county_name" FOREIGN KEY("county_name")
REFERENCES "destinations" ("county_name");

ALTER TABLE "home" ADD CONSTRAINT "fk_home_county_name" FOREIGN KEY("county_name")
REFERENCES "destinations" ("county_name");

