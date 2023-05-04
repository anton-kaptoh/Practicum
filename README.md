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
            <td><a href='churn_model_telecom'>1. Модель оттока клиентов телеком-оператора </br>( Churn model for
                    telecommunications company )</a></td>
            <td>Построена модель оттока клиентов компании предоставляющей услуги интернета и телефонии. Строились
                пайплайны для различных моделей, подбирались гиперпараметры с помощью Optuna.</td>
            <td>classification, pandas, scikit-learn, EDA, pipeline, Optuna, CatBoost, RandomForest, LogisticRegression, Matplotlib, seaborn </td>
        </tr>
        <tr>
            <td><a href='text_toxicity_classification'>2. Модель классификации токсичных комментариев</br>( Text toxicity
                    classification model )</a></td>
            <td>Разработана модель классификации токсичных комментариев. Производился fine-tuning BERT-моделей и
                обучались различные класссические модели на эмбеддингах. </td>
            <td>NLP, classification, DistillBERT, RoBERTa, TensorFlow, PyTorch, transformers, CatBoost, automated moderation</td>
        </tr>
        <tr>
            <td><a href='age_by_face_recognition'>3. Нейросеть для определения возраста по фотографии </br>( Age
                    recognition neural network )</a></td>
            <td>Построена ResNet-модель предсказывающая возраст человека по фото лица. Из моделей с различными
                конфигурациями top-уровней, на разном железе выбиралась с лучшим MAE.</td>
            <td>CV, regression, Keras, image processing </td>
        </tr>
        <tr>
            <td><a href='car_price_prediction'>4. Модель предсказания рыночной цены автомобиля c пробегом </br>( Car price prediction
                    model )</a></td>
            <td>Построена модель для определения стоимости автомобиля на основе LightGBM. Также произведено ее сравнение
                с другими моделями и проанализировано их быстродействие.</td>
            <td> Gradient Boosting, regression, LightGBM, pipeline, scikit-learn, feature_engine, model performance, e-business</td>
        </tr>
        <tr>
            <td><a href='gold_recovery_efficiency_prediction'>5. Исследование технологического процесса очистки золота </br>( Gold
                    recovery process investigation )</a></td>
            <td>Построена модель для определения доли золота на выходе производственного процесса в завивисомсти от
                множества его входных параметров. Исследованы концентрации веществ на разных этапах техпроцесса, проведено тщательно 
                сравнение обучающей и тестовой выборки.</td>
            <td>regression, pipeline, scikit-learn, Gradient Boosting, RandomForestRegressor, Matplotlib, seaborn, industry</td>
        </tr>
        <tr>
            <td><a href='taxi_orders_time_frame_prediciton'>6. Временные ряды - предсказание нагрузки на сервис такси </br>( Time series - hourly taxi service load forecasting )</a></td>
            <td>Построена модель регрессии для временных рядов: модель прогнозирует число заказов на следующий час используя данные за предыдущее время. Подбирались отстающие значения, анализировались тренды и сезонность временных рядов. В итоге лучшие результаты показала линейная регрессия, также проведено сравнение быстродействия моделей.</td>
            <td>time series, regression, pipeline, scikit-learn, statsmodels, LinearRegression, LighGBMRegressor, DecisionTreeRegressor, RandomForestRegressor </td>
        </tr>
        <tr>
            <td><a href='linear_algebra_data_encryption'>7. Линейная алгебра, шифрование личных данных клиентов</br>( Linear algebra, clients data encryption )</a></td>
            <td>Разработан алгоритм для шифрования данных с помощью матричных операций. Доказано аналитчески и экспериментально, что алгоритм не влияет на функцию потерь и качество обучения ML-модели сохраняется.  </td>
            <td>linear algebra, matrix operations, numpy, LinearRegression, regression, pipeline, scikit-learn </td>
        </tr>
        <tr>
            <td><a href='mobile_service_tariff_selection'>8. Модель подбора тарифа для клиента мобильного оператора</br>( Mobile services tariff selection model)</a></td>
            <td>Разработана модель, подбирающая клиенту оптимальный для перехода тариф мобильной связи. Проведено исследование зависимости различных моделей от их гиперапарметров.  </td>
            <td>hyperparameters analysis, LogisticRegression, DecisionTreeClassifier, RandomForestClassifier, scikit-learn matplotlib, seaborn </td>
        </tr>        
        <tr>
            <td><a href='oil_well_region_selection'>9. Выбор региона для разработки нефтяного месторождения (Investigating regions for oil field development) </a></td>
            <td>Разработана бизнес-модель для выбора региона для дальнейшей разработки нефтяных месторождений. Для оценки распределения прибыли  региона используятся техника бутстреп.  </td>
            <td>bootstrap, matplotlib, LinearRegression, regression </td>
        </tr>
    <tbody>
<table>