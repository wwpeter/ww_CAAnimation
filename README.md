# ww_CAAnimation
页面切换的动画
####1.用CATransition实现动画的封装方法如下，每句代码是何意思，请看注释之。

#pragma CATransition动画实现
- (void) transitionWithType:(NSString *) type WithSubtype:(NSString *) subtype ForView : (UIView *) view
{
    //创建CATransition对象
    CATransition *animation = [CATransition animation];
    
    //设置运动时间
    animation.duration = DURATION;
    
    //设置运动type
    animation.type = type;
    if (subtype != nil) {
        
        //设置子类
        animation.subtype = subtype;
    }
    
    //设置运动速度
    animation.timingFunction = UIViewAnimationOptionCurveEaseInOut;
    
    [view.layer addAnimation:animation forKey:@"animation"];
}

代码说明：

    CATransition常用的属性如下：

    duration:设置动画时间

    type:稍后下面会详细的介绍运动类型

    subtype:和type匹配使用，指定运动的方向，下面也会详细介绍

    timingFunction ：动画的运动轨迹，用于变化起点和终点之间的插值计算,形象点说它决定了动画运行的节奏,比如是

    均匀变化(相同时间变化量相同)还是先快后慢,先慢后快还是先慢再快再慢.　　　　
        动画的开始与结束的快慢,有五个预置分别为(下同):
        kCAMediaTimingFunctionLinear 线性,即匀速
        kCAMediaTimingFunctionEaseIn 先慢后快
        kCAMediaTimingFunctionEaseOut 先快后慢
        kCAMediaTimingFunctionEaseInEaseOut 先慢后快再慢
        kCAMediaTimingFunctionDefault 实际效果是动画中间比较快.

2.用UIView的block回调实现动画的代码封装　

#pragma UIView实现动画
- (void) animationWithView : (UIView *)view WithAnimationTransition : (UIViewAnimationTransition) transition
{
    [UIView animateWithDuration:DURATION animations:^{
        [UIView setAnimationCurve:UIViewAnimationCurveEaseInOut];
        [UIView setAnimationTransition:transition forView:view cache:YES];
    }];
}

3.改变View的背景图，便于切换时观察

#pragma 给View添加背景图
-(void)addBgImageWithImageName:(NSString *) imageName
{
     self.view.backgroundColor = [UIColor colorWithPatternImage:[UIImage imageNamed:imageName]];
}
