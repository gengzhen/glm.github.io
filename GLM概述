GLM概述
一、如何使用GLM
GLM是基于 OpenGL 着色语言 (GLSL) 规范的 C++ 数学库。GLM尽可能模GLSL 的向量/矩阵运算方法。
要使用 GLM，请包含glm/glm.hpp。GLM手册的一个例子如下：

#include <glm/glm.hpp>

int foo()
{
    glm::vec4 Position = glm::vec4( glm::vec3( 0.0 ), 1.0 );
    glm::mat4 Model = glm::mat4( 1.0 );
    Model[3] = glm::vec4( 1.0, 1.0, 0.0, 1.0 );
    glm::vec4 Transformed = Model * Position;
    return 0;
}

二、向量和矩阵构造函数
1，向量构造函数：如果向量构造函数有一个标量参数，则它用于将构造向量的所有分量初始化为该标量的值：
    glm::vec4 Position = glm::vec4( glm::vec3( 0 . 0 ), 1 . 0 );

2，矩阵构造函数：如果矩阵构造函数只有一个标量参数，则它用于初始化矩阵对角线上的所有分量，其余分量初始化为0.0f
    glm::mat4 Model = glm::mat4( 1 . 0 );
    
三、矩阵变换
矩阵变换是GLM的扩展。GLM 手册中的示例：
#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>

int foo()
{
    glm::vec4 Position = glm::vec4( glm::vec3( 0.0f ), 1.0f );
    glm::mat4 Model = glm::translate( glm::mat4( 1.0f ), glm::vec3( 1.0f ) );
    glm::vec4 Transformed = Model * Position;
    return 0;
}

四、单位矩阵（两种构造函数）
glm::mat4仅采用单个值的构造函数构造对角矩阵：
glm::mat4 m4( 1 . 0 f ); // 构造单位矩阵
该矩阵沿从左上角到右下角的对角线设置除了1.0f之外的所有零。

默认构造函数glm::mat4()创建对角线为1.0f的对角矩阵，即单位矩阵：
glm::mat4 m4; // 构造单位矩阵

五、矩阵变换函数
1，旋转
    glm::mat4 glm::rotate(
        glm::mat4 const& m,
        float angle,
        glm::vec3 const& axis
        );
2，缩放
    glm::mat4 glm::scale(
        glm::mat4 const& m,
        glm::vec3 const& factors
        );
3，平移
    glm::mat4 glm::translate(
        glm::mat4 const& m,
        glm::vec3 const& translation
        );
        
六、其他矩阵函数
glm::frustum()       //平截头体
glm::ortho()         //正交
glm::lookAt()
glm::perspective()   //透视
glm::project(）      //投射

七、glm::value_ptr
glm::value_ptr采用任何核心模板类型。它返回一个指向对象内存布局的指针。例如，给定
    glm::mat4 m4( 1 . 0 f ); // 构造单位矩阵

表达式
    glm::value_ptr(m4)与&m4[ 0 ][ 0 ]是等价的。

value_ptr()以列优先顺序返回指向矩阵数据的直接指针，这对于将数据上传到 OpenGL 非常有用。

八、glm::value_ptr 示例
把数据传给OpenGL example:

#include <glm/glm.hpp>
#include <glm/gtc/type_ptr.hpp>

void f () {
    glm::vec3 aVector( 3 );
    glm::mat4 someMatrix( 1.0f );
    glUniform3fv( uniformLoc, 1, glm::value_ptr( aVector ) );
    glUniformMatrix4fv( uniformMatrixLoc, 1, GL_FALSE, glm::value_ptr( someMatrix ) );
}

九、矩阵列
glm::mat4中的 每一行和每一列都是从零开始的：
    glm::mat4 m4( 1 . 0 f ); // 构造单位矩阵
    m4[ 0 ]      // 零列
    m4[ 0 ].x    // 同 m4[ 0 ][ 0 ]
     m4[ 0 ].y    // 同 m4[ 0 ][ 1 ]
     m4[ 0 ].z    // 等同于 m4[ 0 ][ 2 ]
     m4[ 0 ].w    // 等同于 m4[ 0 ][ 3 ]

矩阵glm::mat4的 每一列都是一个vec4。

设置整个列，例如用于翻译，


    glm::mat4 m4( 1 . 0 f ); // 构造单位矩阵
    m4[ 3 ] = glm::vec4( vec3( x, y, z ), 1 . 0 f );

十、矩阵缩放示例
When using glm::translate( X, vec3 ), you are multiplying


    X * glm::translate( Identity, vec3 )

This means translate first, then X


十一、 glm::translate
When using glm::translate( X, vec3 ), you are multiplying


    X * glm::translate( Identity, vec3 )

This means translate first, then X

十二、 glm::rotate
When using glm::rotate( X, vec3 ), you are multiplying


    X * glm::rotate( Identity, vec3 )

This means rotate first, then X
十三、 glm::scale
When using glm::scale( X, vec3 ), you are multiplying


    X * glm::scale( Identity, vec3 )

For example,


    glm::mat4 transMatrix = glm::translate(
        glm::mat4( 1.0f ),
        glm::vec3( 0.0f, -0.5f, 0.0f )
        );

    planeModel->mM = glm::scale(  // Scale first
        transMatrix,              // Translate second
        glm::vec3( 100.0f, 100.0f, 100.0f )
        );
        
        
十四、矩阵乘法不可交换
所以常规的 Model-View-Projection 应该反向相乘：

    glm::mat4 MVP = Projection * View * Model;
这意味着首先发生模型转换，然后是视图，最后是投影。

十五、缩放*变换与变换*缩放
两种乘法是不同的。




