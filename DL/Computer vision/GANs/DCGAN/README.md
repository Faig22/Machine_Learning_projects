# DCGAN
## Генерация лиц людей с помощью модели **DCGAN**
### Загрузка данных
Ноутбук был создан непосредственно в ***Kaggle*** и поэтому данные были предоставлены ими и загружены сразу в ноутбук (https://www.kaggle.com/datasets/504743cb487a5aed565ce14238c6343b7d650ffd28c071f03f2fd9b25819e6c9)
Далее изображения были обрезаны, переведены в тензоры и нормализованы, а после через класс **ImageFolder** они были загружены в даталоадер
### Архитектура модели
Модель была взята из статьи (https://arxiv.org/pdf/1511.06434.pdf)
1. Дискриминатор 
   ![image](https://github.com/Faig22/Machine_Learning_projects/assets/95417164/eff61792-89ce-4e01-989e-05eff668aa63)

   Он состоит из 5 ***conv*** - слоев, а на выходе одно число (вероятность того, что поданное изображение фейковое (*0*) или настоящее (*1*))
   
   Для убыстрения этапа обучения добавлен промежуточный слой с *64* каналами (***img_channels***) и убран последний слой с *1024* каналами
   
   Во всех слоях кроме первого и последнего была использована связка ***Conv + BatchNorm + LeakyRelu***. В первом и последнем слое были просто ***conv** слои.
   На выходе стоит сигмоида
   
2. Генератор
   ![image](https://github.com/Faig22/Machine_Learning_projects/assets/95417164/e2ffa45e-8909-4cce-9ec0-d8672dacc219)

   Аналогично дискриминатору он состоит из 5 ***conv*** - слоев, на входе гауссовский шум, на выходе сгенерируемое изображение

   Также для убыстрения обучения был убран первый слой из с *1024* каналами

   Во всех слоях кроме последнего была использована связка ***ConvTranspose2d (увеличивает размер изображений) + BatchNorm + Relu***. В последнем слое был просто ***convTranspose2d** слой.
   На выходе стоит гиперболический тангенс

### Инициализация модели
   Веса модели задаются из нормального распределения с мат. ожиданием 0 и дисперсией 0.02

### Обучение
   
     Гиперпараметры:
     batch_size = 128
     epochs = 30
     noise_dim = 100 - размер шума, подаваемый на вход генератора
     img_size = 64 - размер изображения, который подается на вход дискриминатора
     learning rate = 0.0002 - обучающий коэффициент у оптимизатора Adam
     beta_1 = 0.5 - коэффициент, используемый для вычисления средних значений градиента у оптимизатора Adam
     beta_2 = 0.999 - коэффициент, используемый для вычисления квадратов градиента у оптимизатора Adam
### Результаты
   ![image](https://github.com/Faig22/Machine_Learning_projects/assets/95417164/d8b3b811-e12d-4c37-ae39-e5439d0abec5)


   Отличная генерация)
     
