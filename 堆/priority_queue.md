```C++
class Solution {
public:
    struct unit{ //运算符重载<
        int dis;
        vector<int> coor={0,0};
        unit(int d, vector<int> c){
            dis = d;
            coor = c;
        }

        bool operator>(const unit& u) const{
            if(dis > u.dis)    return true;
            return 0;      //小顶堆
        }
    };

    //方法2
    struct tmp //重写仿函数
    {
        bool operator() (unit a, unit b) 
        {
            return a.dis > b.dis; //大顶堆
        }
    };
    int min(int a, int b){
        return (a<b)? a:b;
    }
    vector<vector<int>> kClosest(vector<vector<int>>& points, int K) {
        priority_queue<unit,vector<unit>,tmp> q;
        for(vector<int> p: points){
            int dis = p[0]*p[0] + p[1]*p[1];
            unit point(dis, p);
            q.push(point);
        }

        vector<vector<int>> res;

        for(int i=0; i<min(K,points.size()); i++){
            res.push_back(q.top().coor);
            q.pop();

        }

        return res;
    }
};
```


## pair的使用

头文件utility

https://blog.csdn.net/sinat_35121480/article/details/54728594