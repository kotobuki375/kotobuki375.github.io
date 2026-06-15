# From Math to Code
* **Notes on linear algebra, geometry, filtering, and their C++ implementations for computer vision and robot perception.**
* 从数学到代码，记录线性代数、几何、滤波等基础内容如何转化为 C++ 实现，并服务于计算机视觉与机器人感知。
*  **💡 深度面试考点（修考高频）：push_back 的扩容机制**
* *vector 的容量是动态增加的，如果我们一直 push_back，内存满了怎么办？*
* 答案：当连续内存不够用时，vector 会在物理内存的其他地方申请一块两倍大（通常是 1.5 倍或 2 倍）的全新连续内存，然后把旧数据拷贝（或移动）到新家，最后释放旧内存。

* 优化小技巧：因为你已经知道了 t 的范围是从 -5 到 5，步长是 0.1，大概要生成 101 个点。如果你在循环前加一句 points.reserve(101);，提前告诉 vector 留出 101 个点的空间，就能完美避免中途频繁搬家扩容造成的性能损耗！实时系统（Real-time System）非常注重这种微小的延迟优化。
* 验证x+y=2;

```cpp
#include <iostream>
#include <vector>

struct Point2D { double x, y; };

int main() {
    std::vector<Point2D> points;
    // 参数 t: 从 -5 到 5
    for (double t = -5; t <= 5; t += 0.1) {
        double x = t;          // 自由变量
        double y = 2 - t;      // 由方程 x + y = 2 解出
        points.push_back({x, y});
    }
    
    // 打印前几个点（验证是否在直线上）
    for (size_t i = 0; i < points.size() && i < 5; ++i) {
        std::cout << "(" << points[i].x << ", " << points[i].y << ")" << std::endl;
    }
    return 0;
}
···
