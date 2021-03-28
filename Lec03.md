# Lecture 3 : Loss Functions and Optimization

## Review

- Challenges of recognition : Semantic Gap

- Data-Driven Approach

- k Nearest Neighbor

- Cross Validation

- Linear Classifier

  - learning `templates` per class

  

Loss Function : **quantifies** how bad our model

Optimization : minimize the loss function

# Loss Function

- $ L = 1/N * \sum L_i(f(x_i, W), y_i) $

- Multiclass SVM Loss (Hinge Loss)

  <img src="https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile3.uf.tistory.com%2Fimage%2F99591E335A15297F13706C" style="zoom:50%;" />

  - $ L_i = \sum_{j\neq y_i} max(0, s_j - s_{y_i} + 1) $
  - **Meaning** : True score >>> all the other score
  - Questions
    - What happends to loss if car scores change a bit?
      A. Doesn't change.
    - What is the min/max possible loss?
      A. min -> Zero, max -> Inf
    - At initialization W is small so all s=0. What is the loss?
      A. # of classes - 1
      - This is used to debugging strategy.
      - should think about what you expect your loss to be.
    - What if the sum was over all classes? (Including j = y_i)
      A. Loss + 1
    - What if we used mean instead of sum?
      A. Doesn't change.
    - What if we used squared...
      A. Different loss function.
      - Why we don't use squared SVM loss?
        --> we don't actually care between being **a little** bit wrong and being **a lot** wrong
  - So, Loss Function is the way that your algorithm **what types of errors you care about** and **what types of errors it should trade off against.**

## Regularization

- Necessary...
  - We really care about performance **on test data**, but the loss function that we learned doesn't meet enough.
  - penalize the model complexity
- Loss = Data Loss(Above) + Regularization Loss
  ![image](https://user-images.githubusercontent.com/48315997/112747342-c4676c00-8fef-11eb-9cce-6da32d8e0bb0.png)
  - Data Loss : Model predictions should match training data
  - Regularization Loss : Model should be "simple", so it works on test data
  - \lambda : regularization strength
- Methods
  <img src="https://blog.kakaocdn.net/dn/bcIedf/btqw5himXFN/qy5nSsXdyAj1ZB1MPeFip1/img.png" style="zoom:50%;" />
  - L2 reg. prefers to spread that influence across all the different values in x
  - L1 reg. prefers sparse matrix

## Softmax Classifier

- SVM : doesn't interpret meaning of score
  - just use how big true score
- $ Softmax = -log(\frac {e^{s_{y_i}}} {\sum_j e^s_j}) $
- Question
  - What is the min/max possible loss L_i?
    A. min -> 0, max -> Inf (in practive, X)
  - usually at initialization W is small so all s=0. What is the loss?
    A. log C -> use to debugging!
  - Suppose I take a datapoint and I jiggle a bit. What happens to the loss in both cases?
    A. SVM -> doesn't change. SVM loss cared about correct score to be grater than incorrect scores.
    Softmax -> try to continually improve every single data point

# Optimization

## Follow the slope

- compute `gradient` of function. 
  - using these gradients to iteratively update W
- calculus to compute an **analytic gradient**
- For debugging -> **gradient check**

## Gradient Descent

- Step size or Learning rate : First Hyperparameter to check!
- Goal : NN to converge

### Stochastic Gradient Descent(SGD)

![스크린샷 2021-03-28 오후 6 39 17](https://user-images.githubusercontent.com/48315997/112748142-e7484f00-8ff4-11eb-9fd6-b0767aaab3c2.png)

- Entire Training data XXXX (expensive)
- Sample some small set (**minibatch**)
