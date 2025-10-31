# DSA-210-term-project
## Project Motivation
In recent years, people’s lifestyles have become increasingly influenced by both environmental and technological factors. Air quality and temperature are key environmental elements that affect how much time people spend outdoors or indoors. When air pollution levels rise or when temperatures become uncomfortable (too cold or too hot), individuals often tend to stay indoors, which can indirectly increase the amount of time they spend using digital devices. 

I am personally curious about how these environmental conditions affect my own daily screen time. Specifically, I want to explore whether there is a measurable correlation between air quality (e.g., PM2.5 levels, overall Air Quality Index), weather conditions (temperature, humidity), and the duration of my daily screen use. This project will allow me to connect environmental data with behavioral patterns through data analysis and hypothesis testing.

My motivation is not only to test this relationship statistically but also to better understand my own habits in the context of environmental changes. If I can identify patterns such as “worse air quality → higher screen time,” it could reveal how much environmental comfort influences daily digital behavior. On a broader scale, similar analyses could provide insights into how environmental quality impacts human lifestyle, productivity, and mental well-being in urban settings.

Through this project, I also aim to practice the complete data science workflow — collecting, cleaning, merging, and analyzing real-world data — and to apply both descriptive and inferential statistical methods to generate meaningful conclusions from personal and public datasets.

## Data Source
- **Personal Data:** My own daily screen time, exported from my phone’s digital wellbeing/screen time report.  
  - I will exclude extreme cases such as exam days or unusual circumstances (e.g., travel days, illness).
- **Environmental Data:** Public air quality and weather data for **Tuzla, Istanbul**.  
  - Air Quality data: [AQICN — Tuzla Station](https://aqicn.org/city/turkey/istanbul/tuzla/)  
  - Weather data (temperature, humidity, etc.): [Open-Meteo API](https://open-meteo.com/) or [OpenAQ](https://openaq.org/)  

## Project Plan
1. Collect my personal screen time data for a selected period (e.g., past 2–3 months).  
2. Download daily air quality (AQI, PM2.5, PM10) and temperature data for the same dates.  
3. Merge datasets on date and create a clean combined dataset.  
4. Conduct exploratory data analysis (EDA) and simple statistical correlation tests.  
5. Exclude outliers (exam days, abnormal cases) to ensure consistency.
