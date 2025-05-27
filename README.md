# Data-Cleaning-Project-MySQL-
Cleaned and standardized a dataset of global tech layoffs to enable accurate trend analysis.

**1. Duplicate Removal**
-- Created staging table and identified duplicates
CREATE TABLE layoffs_staging LIKE layoffs;
INSERT INTO layoffs_staging SELECT * FROM layoffs;

-- Used window function to flag duplicates
SELECT *,
  ROW_NUMBER() OVER(
    PARTITION BY company, location, industry, 
    total_laid_off, percentage_laid_off, 
    `date`, stage, country, funds_raised_millions
  ) AS row_num
FROM layoffs_staging;

-- Created new table and removed duplicates
CREATE TABLE `layoffs_staging2` (
  `company` text,
  `location` text,
  `industry` text,
  `total_laid_off` int DEFAULT NULL,
  `percentage_laid_off` text,
  `date` text,
  `stage` text,
  `country` text,
  `funds_raised_millions` int DEFAULT NULL,
  `row_num` int
);

DELETE FROM layoffs_staging2 WHERE row_num > 1;

**2. Data Standardization**
   -- Fixed inconsistent industry classifications
UPDATE layoffs_staging2
SET industry = 'Crypto'
WHERE industry LIKE 'Crypto%';

-- Corrected country name formatting
UPDATE layoffs_staging2
SET country = TRIM(TRAILING '.' FROM country)
WHERE country LIKE 'United States%';

-- Converted text dates to DATE format
UPDATE layoffs_staging2
SET `date` = STR_TO_DATE(`date`, '%m/%d/%Y');

ALTER TABLE layoffs_staging2
MODIFY COLUMN `date` DATE;

**3. Handling Missing Data**
   -- Populated blank industry fields using self-join
UPDATE layoffs_staging2 t1
JOIN layoffs_staging2 t2 ON t1.company = t2.company
SET t1.industry = t2.industry
WHERE (t1.industry IS NULL OR t1.industry = '')
AND t2.industry IS NOT NULL;

-- Removed records with no layoff data
DELETE FROM layoffs_staging3
WHERE total_laid_off IS NULL
AND percentage_laid_off IS NULL;
