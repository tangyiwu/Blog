## Android布局优化

### 1. 减少嵌套层级

每个view在显示之前，都会有measure、layout、draw这三步，布局层级越深，相应带来的层级遍历消耗时间就越长，因此减少层级可以降低这三步所花的时间。

使用***Layout Inspector***查看布局，分析布局的层级结构。

在**Andriod Studio**的**Tools**下面可以发现***Layout Inspector***

### 2. 去掉多余的背景色

如果Parent和Child的背景色一致，可以去掉Child的背景色，View的背景色的绘制相对耗时较长。

### 3. 布局重用

善用<include/>标签，能够复用布局，减少布局文件。

### 4. 按需加载布局

善用<ViewStub/>标签，在不需要布局时，不会把标签加载进内存，在显示布局时，将需要的布局加载进内存。例如：空白页可以使用这种加载方式，比简单的``View.setVisibility(Gone)``要更高效。





