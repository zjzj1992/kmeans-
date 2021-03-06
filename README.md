# kmeans-
k-means的变种：

1、k-means++：与k-means之间的区别就在于质心的选择机制上，k-means质心选择是随机生成的，所以有时候的聚类结果可能会不好，而k-means++选取质心的方式是：

（1）从数据集中随机选取一个样本作为初始质心

（2）然后计算每个样本与当前已知质心之间的最短距离(即与最近的一个质心的距离)，然后存储到数组D(x)中

（3）接着计算每个样本被选为下一个质心的概率，概率是D(x)中每个样本存储的最短距离的平方除以D(x)中距离平方的累加和，所得的就是该样本作为下一个质心的概率

（4）因为选取每个样本的概率不同，但是概率之和等于1，然后我们可以从0到1之间随机生成一个数，这个数会落在一个区域内，该区域是每个样本作为质心的概率的一个区域，落在哪个区域，那么该区域所对应的点就是下一个质心
举例说明：

![image](https://github.com/zjzj1992/kmeans-/blob/master/images/kjia1.png)

上图中有八个点，
根据第一步的意思，我们可以从这八个点中随机选取一个点作为初始质心，这里我们假设选取的初始质心是6号点
然后根据第二步，要计算每个样本点到这个质心之间的距离，要求是要选择一个样本距离质心最短的距离，但是因为这里只有一个质心，所以最短距离就是样本到当前这个质心之间的距离，每个距离都可以存入D(x)，然后就可以求出所需要的值，如下表所示：

![image](https://github.com/zjzj1992/kmeans-/blob/master/images/kjia2.png)

图中的P(x)就是每个样本会作为下一个质心的概率，最后一行的sum是P(x)的累加和，然后用轮盘法选取第二个质心，方法是随机产生一个0~1之间的数，通过这个随机数去判断，该随机数落在哪个区域那么该点就是下一个质心，由表可以看出前四个点的概率占了90%，也就是说前四个点作为下一个质心的概率是最大的，从图中也可以看出，前四个点距离质心也是最远的那几个，也印证了kmeans++的核心思想：距离已有质心较远的点会有更大的概率会被选为下一个质心，如果k > 2的话，每个样本都会有多个距离，而选取的距离一定是那个距离最短的，然后存入D(x)中
