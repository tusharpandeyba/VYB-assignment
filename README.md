# Indian Dish Nutrition Calculator

## Overview
This project implements an AI-powered solution for calculating the nutritional value of home-cooked Indian dishes per standard serving. Traditional nutrition databases often fall short for Indian cuisine due to household variations in recipes and cooking methods. This solution addresses these challenges through a modular pipeline that intelligently maps ingredients, standardizes measurements, and calculates nutrition values.

## Problem Statement
Given a home-cooked Indian dish name, the system estimates its nutritional value per standard serving by:
1. Retrieving a generic recipe for the dish
2. Converting ingredient quantities to standardized household measurements
3. Mapping ingredients to a nutrition database
4. Standardizing quantities into grams
5. Calculating total nutrition based on ingredient quantities
6. Identifying the food type/category of the dish
7. Calculating nutrition for a standard serving size

## Key Features
- Intelligent ingredient mapping that handles synonyms and spelling variations
- Robust quantity standardization system
- Food type classification for appropriate serving size determination
- Comprehensive error handling for real-world scenarios
- Clear, structured output with nutritional values and ingredient details



## Key Assumptions

1. **Recipe Standardization**:
   - Recipes are assumed to serve 3-4 people unless specified otherwise
   - Water loss during cooking is not factored into calculations at this stage
   - Standard cooking oils and spices are used in typical quantities

2. **Measurement Standardization**:
   - A fixed set of household measurements is used (e.g., 1 katori = ~180g for Wet Sabzi)
   - When exact measurements aren't available, reasonable defaults are applied based on dish type
   - Ingredient densities are approximated based on common cooking practices

3. **Nutritional Calculation**:
   - Nutrition values are linearly scaled from the database's per-100g values
   - Cooking method effects on nutrition (e.g., frying vs. boiling) are not currently modeled
   - When ingredients aren't found in the database, similar alternatives are used with logging

4. **Food Classification**:
   - Dishes are categorized into predefined types (Wet Sabzi, Dry Sabzi, Dal, Non-Veg Curry, etc.)
   - Standard serving sizes vary by food type (e.g., 180g for Wet Sabzi)

## Modularization Approach

The solution is built with clear separation of concerns:

1. **Recipe Fetching Module**: 
   - Responsible for retrieving ingredient lists from an external source or database
   - Handles ingredient quantity parsing and initial normalization
   - Gracefully handles missing/incomplete recipe data

2. **Ingredient Mapping Module**:
   - Matches recipe ingredients to nutrition database entries
   - Implements fuzzy matching for variations in naming
   - Handles synonyms and regional naming differences

3. **Quantity Standardization Module**:
   - Converts various measurement units to standardized household measurements
   - Transforms household measurements to gram weights
   - Handles ambiguous quantity descriptions

4. **Food Classification Module**:
   - Determines the dish category based on ingredients and cooking methods
   - Maps categories to standard serving sizes

5. **Nutrition Calculation Module**:
   - Performs the actual nutritional computation
   - Scales values to standard serving sizes
   - Implements sanity checks for outlier values

## Error Handling Strategy

The system implements robust error handling to address real-world challenges:

1. **Graceful Degradation**: When perfect data isn't available, the system makes reasonable assumptions rather than failing completely
2. **Extensive Logging**: All assumptions, substitutions, and fallbacks are logged for transparency
3. **Confidence Scoring**: Results include a confidence metric based on how many assumptions were made
4. **Validation Logic**: Nutritional outputs are validated against expected ranges to catch calculation errors

## Test Examples

The system has been tested with diverse Indian dishes:

1. **Paneer Butter Masala** (Wet Sabzi)
2. **Aloo Gobi** (Dry Sabzi)
3. **Dal Tadka** (Dal)
4. **Chicken Curry** (Non-Veg Curry)
5. **Vegetable Biryani** (Rice)

See the `tests/test_data` directory for complete input/output examples.

## Future Improvements

1. Incorporate water loss/gain during cooking for more accurate measurements
2. Add regional recipe variations to improve accuracy across India
3. Implement a larger nutrition database with more indigenous ingredients
4. Develop a web interface for easier access
5. Add support for custom recipe inputs from users
