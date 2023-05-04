# Временные ряды - предсказание нагрузки на сервис такси 

Построена модель регрессии для временных рядов: модель прогнозирует число заказов на следующий час используя данные за предыдущее время. Подбирались отстающие значения, анализировались тренды и сезонность временных рядов. В итоге лучшие результаты показала линейная регрессия, также проведено сравнение быстродействия моделей.

## Ссылка на полноценный просмотр ноутбука

https://nbviewer.org/github/anton-kaptoh/Practicum/blob/main/taxi_orders_time_frame_prediciton/TaxiOrdersTimeFramePrediction.ipynb

## Tags
time series, regression, pipeline, scikit-learn, statsmodels, LinearRegression, LighGBMRegressor, DecisionTreeRegressor, RandomForestRegressor