# Practicum
Data Science study projects - Yandex Practicum
<table>
    <tbody>
        <tr>
            <th>Name</th>
            <th>Description</th>
            <th>Tags</th>
        </tr>
        <tr>
            <td><a href='churn_model_telecom'>Модель оттока клиентов телеком-оператора </br>( Churn model for
                    telecommunications company )</a></td>
            <td>Построена модель оттока клиентов компании предоставляющей услуги интернета и телефонии. Строились
                пайплайны для различных моделей, подбирались гиперпараметры с помощью Optuna.</td>
            <td>classification, pandas, scikit-learn, EDA, pipeline, Optuna, CatBoost, RandomForest, LogisticRegression,
                <span style="background-color:rgb(245, 224, 233)">Matplotlib</span>, seaborn </td>
        </tr>
        <tr>
            <td><a href='text_toxicity_classification'>Модель классификации токсичных комментариев</br>( Text toxicity
                    classification model )</a></td>
            <td>Разработана модель классификации токсичных комментариев. Производился fine-tuning BERT-моделей и
                обучались различные класссические модели на эмбеддингах. </td>
            <td>NLP, classification, DistillBERT, RoBERTa, TensorFlow, PyTorch, transformers, CatBoost, automated moderation</td>
        </tr>
        <tr>
            <td><a href='age_by_face_recognition'>Нейросеть для определения возраста по фотографии </br>( Age
                    recognition neural network )</a></td>
            <td>Построена ResNet-модель предсказывающая возраст человека по фото лица. Из моделей с различными
                конфигурациями top-уровней, на разном железе выбиралась с лучшим MAE.</td>
            <td>CV, regression, Keras, image processing </td>
        </tr>
        <tr>
            <td><a href='car_price_prediction'> Модель предсказания рыночной цены автомобиля </br>( Car price prediction
                    model )</a></td>
            <td>Построена модель для определения стоимости автомобиля на основе LightGBM. Также произведено ее сравнение
                с другими моделями и проанализировано их быстродействие.</td>
            <td> Gradient Boosting, regression, LightGBM, pipeline, scikit-learn, feature_engine, model performance, e-business</td>
        </tr>
        <tr>
            <td><a href='gold_recovery_efficiency_prediction'> Исследование технологического процесса очистки золота </br>( Gold
                    recovery process investigation )</a></td>
            <td>Построена модель для определения доли золота на выходе производственного процесса в завивисомсти от
                множества его входных параметров. Исследованы концентрации веществ на разных этапах техпроцесса, проведено тщательно 
                сравнение обучающей и тестовой выборки.</td>
            <td>regression, pipeline, scikit-learn, Gradient Boosting, RandomForestRegressor, <span style="background-color:rgb(245, 224, 233)!important">Matplotlib</span>, seaborn, industry</td>
        </tr>
        <tr>
            <td><a href='gold_recovery_efficiency_prediction'> Временные ряды - предсказание нагрузки на сервис такси </br>( Time series - hourly count of taxi orders forecasting )</a></td>
            <td>Построена модель регрессии для временных рядов: модель прогнозирует число заказов на следующий час используя данные за предыдущее время. Подбирались отстающие значения, анализировались тренды и сезонность временных рядов. В итоге лучшие результаты показала линейная регрессия, также проведено сравнение быстродействия моделей.</td>
            <td>time series, regression, pipeline, scikit-learn, statsmodels, LinearRegression, LighGBMRegressor, DecisionTreeRegressor, RandomForestRegressor </td>
        </tr>
    <tbody>
<table>