{%hackmd BJrTq20hE %}

# ml lecture 3 - 6 Roadmap of Improving Model

[slides: General Guidance](https://drive.google.com/file/d/1WAAYhcuQXoLpQkstUQQREd27szNF8XYu/view?usp=sharing)
[slides: Why Traning Fail](https://drive.google.com/file/d/1B7d23cu-xr0HwizHFYpocUAZNMFBeA8e/view?usp=sharing)
[slides: Adaptive Learning Rate](https://drive.google.com/file/d/1joaubc88xZvmcppWfRH9CTw0fh4gJI07/view?usp=sharing)

## Training
1. Function with Unknow Parameters (所有function中的未知的參數都表示成$\theta$)
   - $y = f_\theta(x)$ 
2. Define **Loss** from Training Data (輸入是一組參數$\theta$)
   - $L(\theta)$ 
3. Optimization (找到使Loss的值最小的$\theta$)
   - $\theta^* = \arg \min_\theta L$ 
- Training data: $\{(x^1, \hat y^1), \;\ldots, (x^N, \hat y^N)\}$
- Testing data: $\{x^{N+1}, \;\ldots, x^{N+M}\}$
- Use $y = f_{\theta^*}(x)$ to label the testing data (把$\theta^*$帶入function的未知參數) 得到 $\{y^{N+1}, \;\ldots, y^{N+M}\}$

## Ganeral Guide
![](https://lh3.googleusercontent.com/lGhY_VMbYHfWLik0TlOuUvMZo5jyEj2lT6e8_y1mXaK37dDH2yIllEeKPFhycKFEyiLdIg2byP02zWn3a3F9YfRj2vSbTyf2uk63dpzbmp7DgEdxWMjNc0g4qqgZSDyG2gDluKVaPbIm5Uz0SYomsm_WUhsJRwnQzuCeSziYnNO3b4jQnXAhdZUL-kbkoh-v83s7uZSnEzNOnFT_I3WH-tQqMyf4h5-YwNBsWZbMAvdTNEMyAnScTEfFnKoJY5eWLInynam0FFbauK1eAF9Op8pVahihYQJr062Tomkdbx-BoMDiDnBxlgk7r6gh4kdPRqkgPg3pWXJvx0Rr1dfYXz79-7WiNAFAR5F2OVGg11RpLGGJP52ymIY03HymSByTL9fjyqgxKMAQenvVMjZIpu1IG4IOyt8aQRDxkwoRbf0vxDyga-R0x2Bxk67s-Hj_ClmplW9ZjQPK7nCy1Tpg4riqC1FM5IXw42qLA8MgFiR07WhmggUXmGOkauej_iyASKFJl5BOv-G0IVyAuBMOHmoOY6q1ZbpLxqMnb6p39_dmj8H4WxNS1LUFmrwsw9o71i0LvkDcma2AgFnCZuksudsDbJtwwmi3paI9OgH6SPh39pvsAU3GgIBpSAL-2Mk8aD5GZ8smCtqNIAtU0X5XXc8T5cRM2iaKafa4EOI7ikJs3_UWWz7SY9v-ETviO_KoPmHPpeYogIsGeBp8QMRgX606=w932-h705-no?authuser=3 =500x)
- Large loss on training data
  - Either model bias or optimization issue
  - 1. Model bias
    - the model is too simple (不存在讓loss低的function, 針不在function set中)
    - Solution: redesign your model to make it more flexible (add features, deep learning)
  - 2. Optimization issue (沒有找使loss低的function) (不一定是overfitting)
    - local minima problem in gradient descent?  (存在讓loss低的function但找不到)
    - solution: TODO: more powerful optimization tech
  - 1 or 2 ?
    - Gaining the insights from comparison
    - Start from shallower networks
    - If deeper networks do not obtain smaller loss on **training data**, then **there is optimization issue**

- Large loss on training data but small loss on testing data
  - Overfitting or mismatch(測試資料突然出現和訓練資料很大的差異，先略過不談)
    - More training data
    - Data augmentation resonably (e.g.把圖片左右翻轉)
    - Constrained model (domain knowledge) (not too much or model bias)
      - Less parameters, sharing parameters (CNN: 較沒彈性，可以針對影像特性))
      - Less features
      - Early stopping
      - Regularization
      - Dropout

#### N-fold Cross Validation
![](https://lh3.googleusercontent.com/f_IvraoxnKdzZwjA6hfDpFYDxQpew5zqHeopJQ6UVhkN6z5tOlTIUb7sWy8wPt3OCmj6YiLfVlHwOzqG2svZzEgu1LbeQoeZiACJDhJaVUEfHyi-j4KXcqxbulHtvAOmWSZq-LKr6arhMjG50jueQIhWDZwQq5B9wlCtXgReCOl9GYuYeJDkBlBDLD939fDsLt-pZp0JYbt61H05EoRQZU8jGr7BB9f0LvVG1ATSnFyioxgm-xJX63IGNdiXymoa8_KtpoP2qQEL_1ZjdLHu77LTBgaLv4C85gnXWig85pEpaNYcdKrNZDM2rsRM02MOL5kD_mxPdOR9SpS9sTxU9b6eApEvyS0dT4QDxaVKmYwNRnMNB362zTnEt8JEMTg1hY-iQKHRTFL4QrQiF-NKtrvztdyomFXKvHDCSlf2sHxgLxmdqYiQUhifswleIuQ9OJyLGjAHA2SNJdBk-uZC1p2asiv2dIjSq_-zkKqNeOywlkghwCI-V-ExIIAdnW95Mo5UyzY_xO_fkTzCZsa8RGbs_61sN17POtrMN9i2t8Gy1hj6JYnaGwfx_SXzkx3LTl8Kiajty634oQ8DX1phNsXPM72bkRAb5BLWl1wWZVY_aEX2dhTZUGksEHijJbUd3dn1NI8gpEKMTVa2Rj6vk713JDbvZAwB6w0BkFxJ96n0-KWOx44kdeMaacCNxRYWRc6urLUtsCb7lTkpSDlZ1Ohz=w883-h627-no?authuser=3 =350x)

## What to do when optimization fails? Analyzing Critical Points
- Optimization fails because
    - critical point
        - local minima
        - saddle point (鞍點: 可能是前後最高但左右有低點)
        ### Tayler Series Approximation, (p. 6)
        > $L(\theta)$ around $\theta=\theta'$ (判斷L的形狀，L在$\theta$附近可以寫成) $$
        > L(\theta) \approx L(\theta') + (\theta-\theta')^Tg + {1 \over 2}(\theta-\theta')^TH(\theta-\theta')
        > $$ where gradient $g$ is a vector (L的一次微分) $$
        > g = \nabla L(\theta'),\; g_i = {\partial \over \partial \theta_i} L(\theta')
        > $$, matrix **Hessian $H$** is a matrix (L的兩次微分) $$
        > H_{ij} = {\partial^2 \over \partial \theta_i \partial \theta_j} L(\theta')
        > $$
        > $\to$ 不用怕saddle point, Hessian的eigenvector可以指引出使loss更小的方向
        > 但實務上不會算出H, 也不太會出現eigenvalue都為正的情況
        > $\to$ 通常還有路可以讓loss下降，所以loss卡住通常是因為saddle point, local minima的情況不多

## What to do when optimization fails? Batch and Momentum
### Small Batch vs Large Batch
- Large Batch (例如沒有用batch) (蓄力時間長, 威力大)
    - ~~Update after seeing all~~
    - Long time for cooldown, but powerful 
- Small Batch (例如一筆資料是一個batch) (冷卻時間短, 較不準)
    - ~~Update for each example~~, Update 20 times in an epoch
    - Short time for cooldown, but noisy
- 若考慮平行運算，大的可能較小的快，但也有平行執行數量限制
- 小的batch size在optimation表現較好，因為Noisy gradient反而幫助traning，較不會卡在同一曲線的local minima
- 小的batch在testing表現較好，以training表現相同的情況之下
    - 因為overfitting, flst minima比sharp minima好(在平坦面上的minima比在峽谷的minima好)
    - 小的batch每次走的方向較不固定，所以較容易走出峽谷
- Batch size is a hyperparameter

#### Summary
| | small | large|
|-|-|-|
| Speed for one update (no parallel) | Faster | Slower |
| Speed for one update(with parallel) |Same|Same(if not too large)|
| Time for one epoch | Slower | ==Faster== |
| Gradient | Noisy | Stable |
| Optimization | ==Better== | Worse |
| Generalization (testing) | ==Better== | Worse |

### Momentum
- 使不要輕易卡在local minima，使用慣性
- Movement not just basedon gradient, but **previous movement**. (考慮過去的gradient, 不只有現在的)
  > #### Vanilla Gradient Descent
  > Movement $m^1 = - \eta g$
  > Move $\theta^1 \leftarrow \theta^0 + m^1$

> ### Gradient Descent + Momentum
> Movement $m^0 = 0$
> Movement $m^1 = \lambda m^0 - \eta g^0$
> Move $\theta^1 \leftarrow \theta^0 + m^1$
> Movement $m^2 = \lambda m^1 - \eta g^1$
> Move $\theta^2 \leftarrow \theta^1 + m^2$
> 
> $m^0 = 0$
> $m^1 = - \eta g^0$
> $m^2 = - \lambda \eta g^0 - \eta g^1 = - \eta g^1 - \lambda \eta g^0$
> (多加上$\lambda * m^1$) (前一個movement乘倍數) (多考慮前面所有gradient的總和)
$\ge$

## Lecture 6: Error Surface is Rugged

### Training Stuck $\neq$ Small Gradient
- 雖然loss不再下降，gradient沒有變得很小
    - 因為gradient在error surface的山谷的兩個谷壁來回震盪，因此loss很少卡在saddle point和local minima, 多數的training還沒到就卡住了
- learning rate connot be one-size-fits-all

#### Adaptive Learning Rate
- Different parameters needs different learning rate
- 山坡大的需要小的learning rate
- $$\theta_i^{t+1} \leftarrow \theta_i^t - {\eta \over \sigma_i^t} g_i^t$$
- learning rate is parameter dependent, $i$表示第i個參數 (多除以一個$\sigma$)

#### Calculate $\sigma$
- Root mean square
    - $\sigma_i^0 = \sqrt {(g_i^0)^2} = |g_i^0|$, $g$ is gradient
    - $\sigma_i^1 = \sqrt {{1 \over 2}[(g_i^0)^2 + (g_i^1)^2]}$
    - $\sigma_i^2 = \sqrt {{1 \over 3}[(g_i^0)^2 + (g_i^1)^2 + (g_i^2)^2]}$
    - $\sigma_i^t = \sqrt {{1 \over t+1} \sum_{j=0}^t(g_i^j)^2}$
    - Used in Adagrad
    - 缺點: learning rate動態調整能力不足, 反應較慢
- RMSProp (改善)
    - $\sigma_i^0 = \sqrt {(g_i^0)^2} = |g_i^0|$
    - $\sigma_i^1 = \sqrt {\alpha (\sigma_i^0)^2 + (1-\alpha)(g_i^1)^2}, 0 < \alpha < 1$, 自行決定現在的gradient重要度，$\alpha$越小表示recent gradient has larger influence
    - $\sigma_i^1 = \sqrt {\alpha (\sigma_i^1)^2 + (1-\alpha)(g_i^2)^2}$
    - $\sigma_i^t = \sqrt {\alpha (\sigma_i^{t-1})^2 + (1-\alpha)(g_i^t)^2}$
    - g變大時會踩剎車將learning rate變小
- Adam: RMSProp + Momentum (結果圖)

#### Learning Rate Scheduling
- 使learning rate和時間有關
- Learning Rate Decay: as the training rate goes, reduce the learning rate
- Warm Up: increase LR and then decrease (in residual network) (in some transformer)
    - explanation: 一開始$\sigma$變動較大，等它統計得較精準後，再讓LR提高

### Summary of Optimization
![](https://lh3.googleusercontent.com/LdlJ0qpeng9coNMkGrsmKaMsFYmympeH-AOMVmWu9v6-3QpBMb-zRRc6tPuC1JNB3HUjzwCWckwifQ5Mbas-TXjSJDrmA087vEY4Nn7Ho8pN1SRnvF-4c3yAdNOyS-jqkER0ETb9gxuc1tu1ccR_tSYnj_Ba_t7H6bmcUsA3CZgbxqVFqLok1IHOTLTOJweFgo4dkBd_AI_YpW_IT8iaT_qrDE9Xb2sZiuBahdE00RjfJMI3O0IvBbO6vUDds6cu5jMvCtWXNwDBbl4R_clviAjexFZa7AshVR-4CgMznt3xi-d4LbtgmAQmJ4N7U4DynYIgWJHKTEVueEE7-WKFCXJAMPVHSmPiWxf39ha7SUCKy0NggOApF28XUrYUq-FmN97WsabqhXaIeXVcf6U2IlXPGrax4JDkLALEf9T_8w9hUxSVQIT9g7NgWWl9ivmBz5DPxAUXhKTkZgggJcmS9s9_8TggBcLtxzZw6XK0wfyo1Sn9N-aq5sfnbvCBzaE13zLJwQi_U8PTjqCqrFxNvdlV-cf3Iq3OeiYE8C2OYQmUdx4Z1CsY1KhXXbOMZIqUSj5Y6-UbXGlFylgJ0ImwGvjTG7EY7OhNJm3wB6FAIIUh9TLm40Epkv8kmsRz34QBhhL_uh4lj_hLDW1vPqtTHR1RUaegtEi-pqXZuSErrciOPMLUV-ZlxROHwKaFGzb9C2J6xgk-A_8tAe-vw2UbYewe=w845-h328-no?authuser=3 =400x)


## Terminologies
- insight 見解
- shallower 較淺的
- augmentation 增加
- seal 封閉
- MNIST (Modified National Institute of Standards and Technology database) 手寫數字影像辨識
- batch 批次
- momentum 動量 衝力 慣性
- vanilla 一般 香草
- DNN (Deep Neural Networks) 深度神經網路
- rugged 崎嶇

###### tags: `ml`