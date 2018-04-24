# VectorAnimator
写个矢量动画：
- 第一步：定义vector_animator,将它作为ImageView的背景，可以把它理解为矢量动画的控制器，它规定了矢量动画的动作。
```
<animated-vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:drawable="@drawable/animated_play">

    <target
        android:name="play"
        android:animation="@animator/animator_play_pause" />

    <target
        android:name="playgroup"
        android:animation="@animator/animator_pause" />

</animated-vector>
```

- 第二步：定义具体动画objectAnimator。在res目录下创建anim目录，不同的矢量动画写法略有不同，包括图形无缝切换、按路径绘制动画、组合。
```
<objectAnimator xmlns:android="http://schemas.android.com/apk/res/android"
    android:duration="500"
    android:valueType="pathType"
    android:propertyName="pathData"
    android:valueFrom="M 3,2 L 7,5 L7,5 L3,5z M 3,8 L7,5 L7,5 L3,5z"
    android:valueTo="M 2,2 L 8,2L8,4 L2,4z M 2,8 L8,8 L8,6 L2,6z"/>
```

- 第三步：定义矢量动画子父关系vector(动画拆分)
```
<vector xmlns:android="http://schemas.android.com/apk/res/android"
    android:width="100dp"
    android:height="100dp"
    android:viewportHeight="100"
    android:viewportWidth="100">
    <group
        android:name="playgroup"
        android:pivotX="5"
        android:pivotY="5">
        <path
            android:name="play"
            android:fillColor="#fff"
            android:pathData="M 3,2 L 7,5 L7,5 L3,5z M 3,8 L7,5 L7,5 L3,5z" />
    </group>
</vector>
```

- 第四步 启动动画
```
Drawable drawable = ivVector.getDrawable();
if (drawable instanceof Animatable)
((Animatable)drawable).start();
```                
