<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UMWTV电影公司 - 圣诞电影狂欢季</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700&family=Playfair+Display:wght@400;500;600;700&display=swap');
        
        :root {
            --primary-color: #9D2932;
            --secondary-color: #D4AF37;
            --dark-color: #000000;
            --light-color: #FFFFFF;
        }
        
        body {
            font-family: 'Montserrat', sans-serif;
            background-color: #0a0a0a;
            color: var(--light-color);
            overflow-x: hidden;
        }
        
        h1, h2, h3, h4, h5, h6 {
            font-family: 'Playfair Display', serif;
        }
        
        .bg-primary {
            background-color: var(--primary-color);
        }
        
        .bg-secondary {
            background-color: var(--secondary-color);
        }
        
        .text-primary {
            color: var(--primary-color);
        }
        
        .text-secondary {
            color: var(--secondary-color);
        }
        
        .border-primary {
            border-color: var(--primary-color);
        }
        
        .border-secondary {
            border-color: var(--secondary-color);
        }
        
        /* 雪花动画 */
        .snowflake {
            position: absolute;
            top: -10%;
            z-index: 10;
            color: white;
            font-size: 1.5rem;
            animation: fall linear forwards;
            opacity: 0.8;
        }
        
        @keyframes fall {
            to {
                transform: translateY(100vh) rotate(720deg);
                opacity: 0;
            }
        }
        
        /* 闪烁效果 */
        .blink {
            animation: blink 2s infinite;
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }
        
        /* 电影卡片悬停效果 */
        .movie-card {
            transition: all 0.3s ease;
        }
        
        .movie-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 15px 30px rgba(212, 175, 55, 0.2);
        }
        
        /* 音频控制器样式 */
        .audio-control {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 1000;
            background: rgba(0, 0, 0, 0.8);
            border-radius: 50px;
            padding: 10px 20px;
            display: flex;
            align-items: center;
            backdrop-filter: blur(10px);
        }
        
        /* 导航栏滚动效果 */
        .navbar {
            transition: all 0.3s ease;
        }
        
        .navbar.scrolled {
            background-color: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
        }
        
        /* 按钮悬停效果 */
        .btn-primary {
            background-color: var(--primary-color);
            color: white;
            transition: all 0.3s ease;
        }
        
        .btn-primary:hover {
            background-color: #7c1f28;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(157, 41, 50, 0.4);
        }
        
        .btn-secondary {
            background-color: var(--secondary-color);
            color: black;
            transition: all 0.3s ease;
        }
        
        .btn-secondary:hover {
            background-color: #c09a2a;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(212, 175, 55, 0.4);
        }
        
        /* 动画入场 */
        .fade-in {
            opacity: 0;
            transform: translateY(20px);
            transition: opacity 0.6s ease, transform 0.6s ease;
        }
        
        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }
        
        /* 3D卡片效果 */
        .card-3d {
            transform-style: preserve-3d;
            transition: transform 0.5s ease;
        }
        
        .card-3d:hover {
            transform: rotateY(10deg) rotateX(5deg);
        }
        
        /* 进度条样式 */
        .progress-bar {
            height: 4px;
            background-color: rgba(255, 255, 255, 0.2);
            border-radius: 2px;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background-color: var(--secondary-color);
            width: 0%;
            transition: width 0.1s linear;
        }
        
        /* 模态框样式 */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            z-index: 2000;
            overflow: auto;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .modal.active {
            opacity: 1;
        }
        
        .modal-content {
            background-color: #1a1a1a;
            margin: 10% auto;
            padding: 20px;
            border: 1px solid var(--secondary-color);
            width: 80%;
            max-width: 700px;
            border-radius: 10px;
            transform: translateY(50px);
            transition: transform 0.3s ease;
        }
        
        .modal.active .modal-content {
            transform: translateY(0);
        }
        
        /* 响应式调整 */
        @media (max-width: 768px) {
            .audio-control {
                bottom: 10px;
                right: 10px;
                padding: 8px 15px;
            }
            
            .modal-content {
                width: 95%;
                margin: 15% auto;
            }
        }
    </style>
</head>
<body>
    <!-- 雪花效果容器 -->
    <div id="snow-container" class="fixed inset-0 pointer-events-none"></div>
    
    <!-- 导航栏 -->
    <nav class="navbar fixed top-0 left-0 w-full z-50 py-4 px-6 flex justify-between items-center">
        <div class="flex items-center">
            <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/8f96cb11c786439584b855c1495dcab8~tplv-a9rns2rl98-image.image?rcl=202512172039516DABD7CA3EFBD5107612&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1768567234&x-signature=gjsx9Pq42YfzXnLaaIe4MTVjAHs%3D" alt="UMWTV Logo" class="h-12 mr-3">
            <span class="text-2xl font-bold text-secondary">UMWTV</span>
        </div>
        <div class="hidden md:flex space-x-8">
            <a href="#home" class="text-white hover:text-secondary transition-colors">首页</a>
            <a href="#movies" class="text-white hover:text-secondary transition-colors">圣诞电影</a>
            <a href="#activities" class="text-white hover:text-secondary transition-colors">互动活动</a>
            <a href="#about" class="text-white hover:text-secondary transition-colors">关于我们</a>
        </div>
        <div class="md:hidden">
            <button id="mobile-menu-button" class="text-white text-2xl">
                <i class="fas fa-bars"></i>
            </button>
        </div>
    </nav>
    
    <!-- 移动端菜单 -->
    <div id="mobile-menu" class="fixed top-0 left-0 w-full h-full bg-black bg-opacity-95 z-40 flex flex-col items-center justify-center hidden">
        <button id="close-menu-button" class="absolute top-6 right-6 text-white text-2xl">
            <i class="fas fa-times"></i>
        </button>
        <div class="flex flex-col space-y-8 text-center">
            <a href="#home" class="text-white text-2xl hover:text-secondary transition-colors mobile-link">首页</a>
            <a href="#movies" class="text-white text-2xl hover:text-secondary transition-colors mobile-link">圣诞电影</a>
            <a href="#activities" class="text-white text-2xl hover:text-secondary transition-colors mobile-link">互动活动</a>
            <a href="#about" class="text-white text-2xl hover:text-secondary transition-colors mobile-link">关于我们</a>
        </div>
    </div>
    
    <!-- 首页 Hero 区域 -->
    <section id="home" class="relative min-h-screen flex items-center justify-center overflow-hidden">
        <div class="absolute inset-0 bg-[url('https://p26-doubao-search-sign.byteimg.com/tos-cn-i-xv4ileqgde/c0ab24ada5e94e689b9d363f9061b75d~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1781527211&x-signature=GAD9t0oxwAIEzkcr1Alih%2B%2BKVbw%3D')] bg-cover bg-center opacity-30"></div>
        <div class="absolute inset-0 bg-gradient-to-b from-black/70 to-black/40"></div>
        
        <div class="container mx-auto px-6 relative z-10 text-center">
            <h1 class="text-5xl md:text-7xl font-bold mb-6 text-secondary fade-in">圣诞电影狂欢季</h1>
            <p class="text-xl md:text-2xl mb-8 max-w-3xl mx-auto fade-in" style="transition-delay: 0.2s;">与UMWTV一起，在这个温馨的节日里，体验最精彩的电影盛宴</p>
            <div class="flex flex-col md:flex-row justify-center gap-4 fade-in" style="transition-delay: 0.4s;">
                <a href="#movies" class="btn-primary px-8 py-3 rounded-full font-semibold text-lg">探索圣诞电影</a>
                <a href="#activities" class="btn-secondary px-8 py-3 rounded-full font-semibold text-lg">参与互动活动</a>
            </div>
        </div>
        
        <div class="absolute bottom-10 left-1/2 transform -translate-x-1/2 animate-bounce">
            <a href="#movies" class="text-white text-4xl">
                <i class="fas fa-chevron-down"></i>
            </a>
        </div>
    </section>
    
    <!-- 圣诞电影推荐 -->
    <section id="movies" class="py-20 bg-black">
        <div class="container mx-auto px-6">
            <h2 class="text-4xl font-bold mb-2 text-center text-secondary fade-in">圣诞精选电影</h2>
            <p class="text-center text-gray-400 mb-12 fade-in" style="transition-delay: 0.2s;">我们为您精选了最适合圣诞观看的经典电影</p>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <!-- 电影卡片 1 -->
                <div class="movie-card bg-gray-900 rounded-lg overflow-hidden shadow-lg fade-in" style="transition-delay: 0.3s;">
                    <div class="relative overflow-hidden h-64">
                        <img src="https://p26-doubao-search-sign.byteimg.com/labis/ca391bda32ccd4f287384c9dd8c82493~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1781527211&x-signature=tkgGBPf9axezQBX%2B8j0fusLjiGw%3D" alt="圣诞怪杰" class="w-full h-full object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-4 right-4 bg-primary text-white px-3 py-1 rounded-full text-sm font-semibold">
                            9.1分
                        </div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-2xl font-bold mb-2 text-secondary">圣诞怪杰</h3>
                        <p class="text-gray-400 mb-4">格林奇试图破坏圣诞却最终被温暖感化，充满幽默与温情，既有搞笑情节又能传递关于爱与包容的正能量。</p>
                        <div class="flex justify-between items-center">
                            <span class="text-gray-500"><i class="fas fa-calendar-alt mr-2"></i>2018</span>
                            <span class="text-gray-500"><i class="fas fa-clock mr-2"></i>1小时30分钟</span>
                        </div>
                        <button class="mt-4 w-full btn-primary py-2 rounded-lg movie-trailer-btn" data-movie="grinch">
                            <i class="fas fa-play mr-2"></i>观看预告片
                        </button>
                    </div>
                </div>
                
                <!-- 电影卡片 2 -->
                <div class="movie-card bg-gray-900 rounded-lg overflow-hidden shadow-lg fade-in" style="transition-delay: 0.4s;">
                    <div class="relative overflow-hidden h-64">
                        <img src="https://p26-doubao-search-sign.byteimg.com/labis/09238240f71d0259aabd4adccf30fbf8~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1781527211&x-signature=0MjDIPEbONRrziBAgmp7dJ%2Bw9O0%3D" alt="圣诞颂歌" class="w-full h-full object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-4 right-4 bg-primary text-white px-3 py-1 rounded-full text-sm font-semibold">
                            8.5分
                        </div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-2xl font-bold mb-2 text-secondary">圣诞颂歌</h3>
                        <p class="text-gray-400 mb-4">改编自查尔斯·狄更斯的经典小说，讲述了一个吝啬鬼在圣诞夜被三个幽灵感化的故事。</p>
                        <div class="flex justify-between items-center">
                            <span class="text-gray-500"><i class="fas fa-calendar-alt mr-2"></i>2009</span>
                            <span class="text-gray-500"><i class="fas fa-clock mr-2"></i>1小时36分钟</span>
                        </div>
                        <button class="mt-4 w-full btn-primary py-2 rounded-lg movie-trailer-btn" data-movie="carol">
                            <i class="fas fa-play mr-2"></i>观看预告片
                        </button>
                    </div>
                </div>
                
                <!-- 电影卡片 3 -->
                <div class="movie-card bg-gray-900 rounded-lg overflow-hidden shadow-lg fade-in" style="transition-delay: 0.5s;">
                    <div class="relative overflow-hidden h-64">
                        <img src="https://p3-doubao-search-sign.byteimg.com/mosaic-legacy/134f0007315cadbab126~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1781527211&x-signature=jywxrBDUxv9maWitwFRpIzxw9rg%3D" alt="一路响叮当" class="w-full h-full object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-4 right-4 bg-primary text-white px-3 py-1 rounded-full text-sm font-semibold">
                            8.4分
                        </div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-2xl font-bold mb-2 text-secondary">一路响叮当</h3>
                        <p class="text-gray-400 mb-4">讲述了一位父亲为了给儿子买圣诞礼物，在圣诞节前夕的疯狂冒险。</p>
                        <div class="flex justify-between items-center">
                            <span class="text-gray-500"><i class="fas fa-calendar-alt mr-2"></i>1996</span>
                            <span class="text-gray-500"><i class="fas fa-clock mr-2"></i>1小时37分钟</span>
                        </div>
                        <button class="mt-4 w-full btn-primary py-2 rounded-lg movie-trailer-btn" data-movie="jingle">
                            <i class="fas fa-play mr-2"></i>观看预告片
                        </button>
                    </div>
                </div>
                
                <!-- 电影卡片 4 -->
                <div class="movie-card bg-gray-900 rounded-lg overflow-hidden shadow-lg fade-in" style="transition-delay: 0.6s;">
                    <div class="relative overflow-hidden h-64">
                        <img src="https://p3-doubao-search-sign.byteimg.com/mosaic-legacy/134e0006e76dec9e225d~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1781527211&x-signature=h5PlUg5BQlZOvV4v7uNJGmEdLYU%3D" alt="红鼻子驯鹿鲁道夫" class="w-full h-full object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-4 right-4 bg-primary text-white px-3 py-1 rounded-full text-sm font-semibold">
                            8.7分
                        </div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-2xl font-bold mb-2 text-secondary">红鼻子驯鹿鲁道夫</h3>
                        <p class="text-gray-400 mb-4">讲述了一只红鼻子驯鹿因为自己的特殊外表而遭遇排挤，最终成为圣诞老人最得力助手的故事。</p>
                        <div class="flex justify-between items-center">
                            <span class="text-gray-500"><i class="fas fa-calendar-alt mr-2"></i>1964</span>
                            <span class="text-gray-500"><i class="fas fa-clock mr-2"></i>55分钟</span>
                        </div>
                        <button class="mt-4 w-full btn-primary py-2 rounded-lg movie-trailer-btn" data-movie="rudolph">
                            <i class="fas fa-play mr-2"></i>观看预告片
                        </button>
                    </div>
                </div>
                
                <!-- 电影卡片 5 -->
                <div class="movie-card bg-gray-900 rounded-lg overflow-hidden shadow-lg fade-in" style="transition-delay: 0.7s;">
                    <div class="relative overflow-hidden h-64">
                        <img src="https://p3-doubao-search-sign.byteimg.com/labis/2253c44ab2fd272f5d92e565a587ce61~tplv-be4g95zd3a-image.jpeg?rk3s=542c0f93&x-expires=1781527211&x-signature=p9NhELoqQ1Yb0D7G%2BZumwvXsNiI%3D" alt="圣诞奇妙公司" class="w-full h-full object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-4 right-4 bg-primary text-white px-3 py-1 rounded-full text-sm font-semibold">
                            8.2分
                        </div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-2xl font-bold mb-2 text-secondary">圣诞奇妙公司</h3>
                        <p class="text-gray-400 mb-4">圣诞老人和他的精灵们在圣诞节前夕的冒险故事，充满奇幻与温馨。</p>
                        <div class="flex justify-between items-center">
                            <span class="text-gray-500"><i class="fas fa-calendar-alt mr-2"></i>2017</span>
                            <span class="text-gray-500"><i class="fas fa-clock mr-2"></i>1小时45分钟</span>
                        </div>
                        <button class="mt-4 w-full btn-primary py-2 rounded-lg movie-trailer-btn" data-movie="santa">
                            <i class="fas fa-play mr-2"></i>观看预告片
                        </button>
                    </div>
                </div>
                
                <!-- 电影卡片 6 -->
                <div class="movie-card bg-gray-900 rounded-lg overflow-hidden shadow-lg fade-in" style="transition-delay: 0.8s;">
                    <div class="relative overflow-hidden h-64">
                        <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/57b4483bc3c14f2ab35ac9ff9329e6a9~tplv-a9rns2rl98-image.image?rcl=202512172039516DABD7CA3EFBD5107612&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1768567233&x-signature=zTm9tBfyQTLIwTvfkRrBNV7nR54%3D" alt="圣诞夜语" class="w-full h-full object-cover transition-transform duration-500 hover:scale-110">
                        <div class="absolute top-4 right-4 bg-primary text-white px-3 py-1 rounded-full text-sm font-semibold">
                            8.9分
                        </div>
                    </div>
                    <div class="p-6">
                        <h3 class="text-2xl font-bold mb-2 text-secondary">圣诞夜语</h3>
                        <p class="text-gray-400 mb-4">一部温馨的圣诞主题电影，讲述了在圣诞夜发生的一系列感人故事。</p>
                        <div class="flex justify-between items-center">
                            <span class="text-gray-500"><i class="fas fa-calendar-alt mr-2"></i>2023</span>
                            <span class="text-gray-500"><i class="fas fa-clock mr-2"></i>1小时50分钟</span>
                        </div>
                        <button class="mt-4 w-full btn-primary py-2 rounded-lg movie-trailer-btn" data-movie="night">
                            <i class="fas fa-play mr-2"></i>观看预告片
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 互动活动区 -->
    <section id="activities" class="py-20 bg-gradient-to-b from-black to-gray-900">
        <div class="container mx-auto px-6">
            <h2 class="text-4xl font-bold mb-2 text-center text-secondary fade-in">圣诞互动活动</h2>
            <p class="text-center text-gray-400 mb-12 fade-in" style="transition-delay: 0.2s;">参与我们的互动活动，赢取精彩好礼</p>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
                <!-- 圣诞问答 -->
                <div class="bg-gray-800 rounded-lg p-8 shadow-lg fade-in card-3d" style="transition-delay: 0.3s;">
                    <div class="flex items-center mb-6">
                        <div class="bg-secondary rounded-full p-4 mr-4">
                            <i class="fas fa-question text-3xl text-black"></i>
                        </div>
                        <h3 class="text-2xl font-bold text-secondary">圣诞知识问答</h3>
                    </div>
                    <p class="text-gray-300 mb-6">测试你对圣诞节和圣诞电影的了解，赢取精美礼品！</p>
                    <div id="quiz-container">
                        <div id="quiz-start" class="text-center">
                            <p class="mb-6">点击开始按钮，挑战你的圣诞知识！</p>
                            <button id="start-quiz" class="btn-secondary px-8 py-3 rounded-full font-semibold">
                                开始挑战
                            </button>
                        </div>
                        
                        <div id="quiz-questions" class="hidden">
                            <div id="question-container" class="mb-6">
                                <h4 id="question-text" class="text-xl font-semibold mb-4 text-white"></h4>
                                <div id="options-container" class="space-y-3">
                                    <!-- 选项将通过JS动态生成 -->
                                </div>
                            </div>
                            <div class="flex justify-between items-center">
                                <span id="question-number" class="text-gray-400">问题 1/5</span>
                                <div class="progress-bar w-full">
                                    <div id="progress" class="progress"></div>
                                </div>
                            </div>
                        </div>
                        
                        <div id="quiz-results" class="hidden text-center">
                            <h4 class="text-2xl font-bold mb-4 text-secondary">测验结果</h4>
                            <p class="text-xl mb-2">你的得分：<span id="score" class="text-secondary font-bold">0</span>/5</p>
                            <p id="result-message" class="mb-6"></p>
                            <button id="restart-quiz" class="btn-primary px-8 py-3 rounded-full font-semibold">
                                再来一次
                            </button>
                        </div>
                    </div>
                </div>
                
                <!-- 电影角色装扮滤镜 -->
                <div class="bg-gray-800 rounded-lg p-8 shadow-lg fade-in card-3d" style="transition-delay: 0.4s;">
                    <div class="flex items-center mb-6">
                        <div class="bg-secondary rounded-full p-4 mr-4">
                            <i class="fas fa-camera text-3xl text-black"></i>
                        </div>
                        <h3 class="text-2xl font-bold text-secondary">圣诞角色滤镜</h3>
                    </div>
                    <p class="text-gray-300 mb-6">上传你的照片，变身圣诞电影中的经典角色！</p>
                    
                    <div class="text-center">
                        <div id="filter-preview" class="relative w-full h-64 bg-gray-700 rounded-lg mb-6 flex items-center justify-center overflow-hidden">
                            <i class="fas fa-image text-5xl text-gray-500"></i>
                            <p class="absolute bottom-4 text-gray-400">预览区域</p>
                        </div>
                        
                        <div class="mb-6">
                            <label for="character-select" class="block text-gray-300 mb-2 text-left">选择角色：</label>
                            <select id="character-select" class="w-full bg-gray-700 text-white p-3 rounded-lg">
                                <option value="santa">圣诞老人</option>
                                <option value="grinch">圣诞怪杰</option>
                                <option value="elf">圣诞精灵</option>
                                <option value="rudolph">红鼻子驯鹿</option>
                            </select>
                        </div>
                        
                        <div class="flex flex-col md:flex-row gap-4 justify-center">
                            <button id="upload-photo" class="btn-primary px-6 py-3 rounded-lg font-semibold">
                                <i class="fas fa-upload mr-2"></i>上传照片
                            </button>
                            <button id="apply-filter" class="btn-secondary px-6 py-3 rounded-lg font-semibold">
                                <i class="fas fa-magic mr-2"></i>应用滤镜
                            </button>
                        </div>
                        
                        <input type="file" id="photo-input" class="hidden" accept="image/*">
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 关于我们 -->
    <section id="about" class="py-20 bg-black">
        <div class="container mx-auto px-6">
            <h2 class="text-4xl font-bold mb-2 text-center text-secondary fade-in">关于UMWTV</h2>
            <p class="text-center text-gray-400 mb-12 fade-in" style="transition-delay: 0.2s;">南非领先的电影制作公司</p>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-12 items-center">
                <div class="fade-in" style="transition-delay: 0.3s;">
                    <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/4bfbc08cbce74d4f8857faba100482b3~tplv-a9rns2rl98-image.image?rcl=202512172039516DABD7CA3EFBD5107612&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1768567234&x-signature=p7IpQTBsvv1ofyRKbe994VyG4hc%3D" alt="UMWTV电影公司" class="rounded-lg shadow-lg w-full">
                </div>
                
                <div class="fade-in" style="transition-delay: 0.4s;">
                    <h3 class="text-2xl font-bold mb-4 text-secondary">我们的故事</h3>
                    <p class="text-gray-300 mb-6">UMWTV是南非领先的电影制作公司，致力于创作高质量、有深度的电影作品。我们的团队由行业内最优秀的专业人士组成，包括导演、编剧、摄影师和制作人。</p>
                    
                    <h3 class="text-2xl font-bold mb-4 text-secondary">我们的使命</h3>
                    <p class="text-gray-300 mb-6">我们的使命是通过电影讲述引人入胜的故事，触动观众的情感，同时展示南非丰富的文化多样性和创造力。我们相信电影的力量可以连接不同的文化和社区，促进理解和包容。</p>
                    
                    <div class="flex space-x-4">
                        <a href="#" class="bg-gray-800 hover:bg-gray-700 text-white p-3 rounded-full transition-colors">
                            <i class="fab fa-facebook-f"></i>
                        </a>
                        <a href="#" class="bg-gray-800 hover:bg-gray-700 text-white p-3 rounded-full transition-colors">
                            <i class="fab fa-twitter"></i>
                        </a>
                        <a href="#" class="bg-gray-800 hover:bg-gray-700 text-white p-3 rounded-full transition-colors">
                            <i class="fab fa-instagram"></i>
                        </a>
                        <a href="#" class="bg-gray-800 hover:bg-gray-700 text-white p-3 rounded-full transition-colors">
                            <i class="fab fa-youtube"></i>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <!-- 页脚 -->
    <footer class="bg-gray-900 py-12">
        <div class="container mx-auto px-6">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                <div>
                    <div class="flex items-center mb-4">
                        <img src="https://p3-flow-imagex-sign.byteimg.com/tos-cn-i-a9rns2rl98/rc/pc/super_tool/8f96cb11c786439584b855c1495dcab8~tplv-a9rns2rl98-image.image?rcl=202512172039516DABD7CA3EFBD5107612&rk3s=8e244e95&rrcfp=f06b921b&x-expires=1768567234&x-signature=gjsx9Pq42YfzXnLaaIe4MTVjAHs%3D" alt="UMWTV Logo" class="h-10 mr-3">
                        <span class="text-xl font-bold text-secondary">UMWTV</span>
                    </div>
                    <p class="text-gray-400">南非领先的电影制作公司，致力于创作高质量的电影作品。</p>
                </div>
                
                <div>
                    <h4 class="text-lg font-semibold text-white mb-4">快速链接</h4>
                    <ul class="space-y-2">
                        <li><a href="#home" class="text-gray-400 hover:text-secondary transition-colors">首页</a></li>
                        <li><a href="#movies" class="text-gray-400 hover:text-secondary transition-colors">圣诞电影</a></li>
                        <li><a href="#activities" class="text-gray-400 hover:text-secondary transition-colors">互动活动</a></li>
                        <li><a href="#about" class="text-gray-400 hover:text-secondary transition-colors">关于我们</a></li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-semibold text-white mb-4">联系我们</h4>
                    <ul class="space-y-2 text-gray-400">
                        <li><i class="fas fa-map-marker-alt mr-2 text-secondary"></i>约翰内斯堡，南非</li>
                        <li><i class="fas fa-phone mr-2 text-secondary"></i>+27 11 123 4567</li>
                        <li><i class="fas fa-envelope mr-2 text-secondary"></i>info@umwtv.co.za</li>
                    </ul>
                </div>
                
                <div>
                    <h4 class="text-lg font-semibold text-white mb-4">订阅通讯</h4>
                    <p class="text-gray-400 mb-4">订阅我们的通讯，获取最新电影资讯和活动信息。</p>
                    <form id="subscribe-form" class="flex">
                        <input type="email" placeholder="您的邮箱地址" class="bg-gray-800 text-white px-4 py-2 rounded-l-lg focus:outline-none flex-1">
                        <button type="submit" class="bg-secondary text-black px-4 py-2 rounded-r-lg hover:bg-opacity-90 transition-colors">
                            <i class="fas fa-paper-plane"></i>
                        </button>
                    </form>
                </div>
            </div>
            
            <div class="border-t border-gray-800 mt-12 pt-8 text-center text-gray-500">
                <p>&copy; 2025 UMWTV电影公司. 保留所有权利.</p>
            </div>
        </div>
    </footer>
    
    <!-- 音频控制器 -->
    <div class="audio-control">
        <button id="play-pause-btn" class="text-white mr-4">
            <i class="fas fa-play"></i>
        </button>
        <div class="flex flex-col mr-4">
            <span id="current-song" class="text-white text-sm">Jingle Bell Rock</span>
            <div class="progress-bar w-32">
                <div id="audio-progress" class="progress"></div>
            </div>
        </div>
        <button id="next-song-btn" class="text-white">
            <i class="fas fa-forward"></i>
        </button>
    </div>
    
    <!-- 电影预告片模态框 -->
    <div id="trailer-modal" class="modal">
        <div class="modal-content">
            <span class="close-modal absolute top-4 right-4 text-white text-2xl cursor-pointer">&times;</span>
            <div class="aspect-w-16 aspect-h-9">
                <div id="trailer-player" class="w-full h-96 bg-black rounded-lg flex items-center justify-center">
                    <i class="fas fa-spinner fa-spin text-4xl text-secondary"></i>
                </div>
            </div>
            <h3 id="trailer-title" class="text-2xl font-bold mt-4 text-secondary"></h3>
            <p id="trailer-description" class="text-gray-400 mt-2"></p>
        </div>
    </div>
    
    <script>
        // 圣诞歌曲列表
        const christmasSongs = [
            {
                title: "Jingle Bell Rock",
                artist: "Bobby Helms"
            },
            {
                title: "Last Christmas",
                artist: "Wham!"
            },
            {
                title: "All I Want for Christmas Is You",
                artist: "Mariah Carey"
            },
            {
                title: "Santa Tell Me",
                artist: "Ariana Grande"
            },
            {
                title: "Underneath the Tree",
                artist: "Kelly Clarkson"
            }
        ];
        
        // 电影数据
        const moviesData = {
            grinch: {
                title: "圣诞怪杰",
                description: "格林奇试图破坏圣诞却最终被温暖感化，充满幽默与温情，既有搞笑情节又能传递关于爱与包容的正能量。"
            },
            carol: {
                title: "圣诞颂歌",
                description: "改编自查尔斯·狄更斯的经典小说，讲述了一个吝啬鬼在圣诞夜被三个幽灵感化的故事。"
            },
            jingle: {
                title: "一路响叮当",
                description: "讲述了一位父亲为了给儿子买圣诞礼物，在圣诞节前夕的疯狂冒险。"
            },
            rudolph: {
                title: "红鼻子驯鹿鲁道夫",
                description: "讲述了一只红鼻子驯鹿因为自己的特殊外表而遭遇排挤，最终成为圣诞老人最得力助手的故事。"
            },
            santa: {
                title: "圣诞奇妙公司",
                description: "圣诞老人和他的精灵们在圣诞节前夕的冒险故事，充满奇幻与温馨。"
            },
            night: {
                title: "圣诞夜语",
                description: "一部温馨的圣诞主题电影，讲述了在圣诞夜发生的一系列感人故事。"
            }
        };
        
        // 问答题目
        const quizQuestions = [
            {
                question: "《圣诞怪杰》中，格林奇为什么讨厌圣诞节？",
                options: [
                    "因为他的鼻子对圣诞装饰过敏",
                    "因为他从小被嘲笑，没有感受过圣诞的温暖",
                    "因为他不喜欢噪音",
                    "因为他想要所有的圣诞礼物"
                ],
                correctAnswer: 1
            },
            {
                question: "电影《真爱至上》中包含了多少个独立的爱情故事？",
                options: [
                    "5个",
                    "7个",
                    "9个",
                    "10个"
                ],
                correctAnswer: 3
            },
            {
                question: "《小鬼当家》中，凯文用什么方式阻止了小偷进入家中？",
                options: [
                    "报警",
                    "设置各种陷阱",
                    "找邻居帮忙",
                    "藏起来不出声"
                ],
                correctAnswer: 1
            },
            {
                question: "《极地特快》中，小男孩克劳斯在圣诞前夜乘坐火车去了哪里？",
                options: [
                    "北极",
                    "圣诞老人的 workshop",
                    "圣诞镇",
                    "雪人王国"
                ],
                correctAnswer: 0
            },
            {
                question: "《圣诞颂歌》中的主角斯克鲁奇是一个什么样的人？",
                options: [
                    "善良的慈善家",
                    "吝啬的商人",
                    "快乐的邮递员",
                    "贫穷的艺术家"
                ],
                correctAnswer: 1
            }
        ];
        
        // DOM元素
        const snowContainer = document.getElementById('snow-container');
        const navbar = document.querySelector('.navbar');
        const mobileMenuButton = document.getElementById('mobile-menu-button');
        const closeMenuButton = document.getElementById('close-menu-button');
        const mobileMenu = document.getElementById('mobile-menu');
        const mobileLinks = document.querySelectorAll('.mobile-link');
        const playPauseBtn = document.getElementById('play-pause-btn');
        const nextSongBtn = document.getElementById('next-song-btn');
        const currentSongElement = document.getElementById('current-song');
        const audioProgress = document.getElementById('audio-progress');
        const progressElement = document.getElementById('progress');
        const startQuizBtn = document.getElementById('start-quiz');
        const quizStart = document.getElementById('quiz-start');
        const quizQuestionsElement = document.getElementById('quiz-questions');
        const quizResults = document.getElementById('quiz-results');
        const questionText = document.getElementById('question-text');
        const optionsContainer = document.getElementById('options-container');
        const questionNumber = document.getElementById('question-number');
        const scoreElement = document.getElementById('score');
        const resultMessage = document.getElementById('result-message');
        const restartQuizBtn = document.getElementById('restart-quiz');
        const uploadPhotoBtn = document.getElementById('upload-photo');
        const photoInput = document.getElementById('photo-input');
        const characterSelect = document.getElementById('character-select');
        const applyFilterBtn = document.getElementById('apply-filter');
        const filterPreview = document.getElementById('filter-preview');
        const subscribeForm = document.getElementById('subscribe-form');
        const trailerModal = document.getElementById('trailer-modal');
        const closeModal = document.querySelector('.close-modal');
        const trailerPlayer = document.getElementById('trailer-player');
        const trailerTitle = document.getElementById('trailer-title');
        const trailerDescription = document.getElementById('trailer-description');
        const movieTrailerBtns = document.querySelectorAll('.movie-trailer-btn');
        
        // 音频播放状态
        let isPlaying = false;
        let currentSongIndex = 0;
        
        // 问答游戏状态
        let currentQuestionIndex = 0;
        let score = 0;
        
        // 初始化
        document.addEventListener('DOMContentLoaded', function() {
            createSnowflakes();
            setupScrollEffects();
            setupEventListeners();
            updateCurrentSongDisplay();
        });
        
        // 创建雪花效果
        function createSnowflakes() {
            const snowflakeCount = window.innerWidth < 768 ? 30 : 50;
            
            for (let i = 0; i < snowflakeCount; i++) {
                const snowflake = document.createElement('div');
                snowflake.classList.add('snowflake');
                
                // 随机雪花图标
                const snowflakeIcons = ['❄️', '❅', '❆', '✦', '✧'];
                const randomIcon = snowflakeIcons[Math.floor(Math.random() * snowflakeIcons.length)];
                snowflake.textContent = randomIcon;
                
                // 随机位置和大小
                const size = Math.random() * 20 + 10;
                snowflake.style.fontSize = `${size}px`;
                snowflake.style.left = `${Math.random() * 100}vw`;
                snowflake.style.opacity = Math.random() * 0.8 + 0.2;
                
                // 随机动画持续时间
                const duration = Math.random() * 10 + 10;
                snowflake.style.animationDuration = `${duration}s`;
                snowflake.style.animationDelay = `${Math.random() * 10}s`;
                
                snowContainer.appendChild(snowflake);
            }
        }
        
        // 设置滚动效果
        function setupScrollEffects() {
            // 导航栏滚动效果
            window.addEventListener('scroll', function() {
                if (window.scrollY > 50) {
                    navbar.classList.add('scrolled');
                } else {
                    navbar.classList.remove('scrolled');
                }
                
                // 淡入元素
                const fadeElements = document.querySelectorAll('.fade-in');
                fadeElements.forEach(element => {
                    const elementTop = element.getBoundingClientRect().top;
                    const elementBottom = element.getBoundingClientRect().bottom;
                    
                    if (elementTop < window.innerHeight - 100 && elementBottom > 0) {
                        element.classList.add('visible');
                    }
                });
            });
            
            // 初始触发一次滚动事件，以显示首屏元素
            window.dispatchEvent(new Event('scroll'));
        }
        
        // 设置事件监听器
        function setupEventListeners() {
            // 移动端菜单
            mobileMenuButton.addEventListener('click', function() {
                mobileMenu.classList.remove('hidden');
                document.body.style.overflow = 'hidden';
            });
            
            closeMenuButton.addEventListener('click', function() {
                mobileMenu.classList.add('hidden');
                document.body.style.overflow = 'auto';
            });
            
            mobileLinks.forEach(link => {
                link.addEventListener('click', function() {
                    mobileMenu.classList.add('hidden');
                    document.body.style.overflow = 'auto';
                });
            });
            
            // 音频控制
            playPauseBtn.addEventListener('click', togglePlayPause);
            nextSongBtn.addEventListener('click', playNextSong);
            
            // 问答游戏
            startQuizBtn.addEventListener('click', startQuiz);
            restartQuizBtn.addEventListener('click', restartQuiz);
            
            // 照片上传和滤镜
            uploadPhotoBtn.addEventListener('click', function() {
                photoInput.click();
            });
            
            photoInput.addEventListener('change', handlePhotoUpload);
            applyFilterBtn.addEventListener('click', applyFilter);
            
            // 订阅表单
            subscribeForm.addEventListener('submit', function(e) {
                e.preventDefault();
                const emailInput = this.querySelector('input[type="email"]');
                if (emailInput.value.trim() !== '') {
                    alert('感谢您的订阅！');
                    emailInput.value = '';
                } else {
                    alert('请输入有效的邮箱地址');
                }
            });
            
            // 电影预告片
            movieTrailerBtns.forEach(btn => {
                btn.addEventListener('click', function() {
                    const movieId = this.getAttribute('data-movie');
                    showTrailer(movieId);
                });
            });
            
            closeModal.addEventListener('click', closeTrailerModal);
            trailerModal.addEventListener('click', function(e) {
                if (e.target === trailerModal) {
                    closeTrailerModal();
                }
            });
            
            // 平滑滚动
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function(e) {
                    e.preventDefault();
                    const targetId = this.getAttribute('href');
                    const targetElement = document.querySelector(targetId);
                    
                    if (targetElement) {
                        window.scrollTo({
                            top: targetElement.offsetTop - 80,
                            behavior: 'smooth'
                        });
                    }
                });
            });
        }
        
        // 音频控制函数
        function togglePlayPause() {
            if (isPlaying) {
                playPauseBtn.innerHTML = '<i class="fas fa-play"></i>';
            } else {
                playPauseBtn.innerHTML = '<i class="fas fa-pause"></i>';
                simulateAudioPlayback();
            }
            isPlaying = !isPlaying;
        }
        
        function playNextSong() {
            currentSongIndex = (currentSongIndex + 1) % christmasSongs.length;
            updateCurrentSongDisplay();
            
            if (isPlaying) {
                simulateAudioPlayback();
            }
        }
        
        function updateCurrentSongDisplay() {
            const currentSong = christmasSongs[currentSongIndex];
            currentSongElement.textContent = `${currentSong.title} - ${currentSong.artist}`;
        }
        
        function simulateAudioPlayback() {
            // 模拟音频播放进度
            let progress = 0;
            audioProgress.style.width = '0%';
            
            const interval = setInterval(() => {
                if (!isPlaying) {
                    clearInterval(interval);
                    return;
                }
                
                progress += 0.5;
                audioProgress.style.width = `${progress}%`;
                
                if (progress >= 100) {
                    clearInterval(interval);
                    playNextSong();
                }
            }, 100);
        }
        
        // 问答游戏函数
        function startQuiz() {
            quizStart.classList.add('hidden');
            quizQuestionsElement.classList.remove('hidden');
            currentQuestionIndex = 0;
            score = 0;
            showQuestion(currentQuestionIndex);
        }
        
        function showQuestion(index) {
            const question = quizQuestions[index];
            questionText.textContent = question.question;
            questionNumber.textContent = `问题 ${index + 1}/${quizQuestions.length}`;
            progressElement.style.width = `${(index / quizQuestions.length) * 100}%`;
            
            optionsContainer.innerHTML = '';
            question.options.forEach((option, i) => {
                const optionButton = document.createElement('button');
                optionButton.classList.add('w-full', 'text-left', 'p-3', 'bg-gray-700', 'hover:bg-gray-600', 'rounded-lg', 'transition-colors');
                optionButton.textContent = option;
                optionButton.addEventListener('click', () => checkAnswer(i));
                optionsContainer.appendChild(optionButton);
            });
        }
        
        function checkAnswer(selectedIndex) {
            const currentQuestion = quizQuestions[currentQuestionIndex];
            
            if (selectedIndex === currentQuestion.correctAnswer) {
                score++;
            }
            
            currentQuestionIndex++;
            
            if (currentQuestionIndex < quizQuestions.length) {
                setTimeout(() => showQuestion(currentQuestionIndex), 500);
            } else {
                showResults();
            }
        }
        
        function showResults() {
            quizQuestionsElement.classList.add('hidden');
            quizResults.classList.remove('hidden');
            scoreElement.textContent = score;
            
            if (score === quizQuestions.length) {
                resultMessage.textContent = '太棒了！你是圣诞电影专家！';
            } else if (score >= quizQuestions.length / 2) {
                resultMessage.textContent = '不错的表现！你对圣诞电影有很好的了解。';
            } else {
                resultMessage.textContent = '继续加油！多看看圣诞电影吧！';
            }
        }
        
        function restartQuiz() {
            quizResults.classList.add('hidden');
            startQuiz();
        }
        
        // 照片上传和滤镜函数
        function handlePhotoUpload(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    img.classList.add('w-full', 'h-full', 'object-cover');
                    
                    filterPreview.innerHTML = '';
                    filterPreview.appendChild(img);
                };
                reader.readAsDataURL(file);
            }
        }
        
        function applyFilter() {
            const character = characterSelect.value;
            const filterPreviewImg = filterPreview.querySelector('img');
            
            if (!filterPreviewImg) {
                alert('请先上传照片');
                return;
            }
            
            // 应用滤镜效果
            filterPreviewImg.style.filter = getCharacterFilter(character);
            
            // 添加一些动画效果
            filterPreviewImg.classList.add('animate-pulse');
            setTimeout(() => {
                filterPreviewImg.classList.remove('animate-pulse');
            }, 1000);
        }
        
        function getCharacterFilter(character) {
            switch (character) {
                case 'santa':
                    return 'brightness(1.2) saturate(1.5) hue-rotate(20deg)';
                case 'grinch':
                    return 'sepia(0.5) hue-rotate(120deg) saturate(2)';
                case 'elf':
                    return 'brightness(1.3) saturate(1.8) hue-rotate(-30deg)';
                case 'rudolph':
                    return 'sepia(0.7) hue-rotate(30deg) saturate(1.5)';
                default:
                    return 'none';
            }
        }
        
        // 电影预告片函数
        function showTrailer(movieId) {
            const movie = moviesData[movieId];
            if (movie) {
                trailerTitle.textContent = movie.title;
                trailerDescription.textContent = movie.description;
                
                // 显示预告片占位符
                trailerPlayer.innerHTML = `<div class="w-full h-full flex items-center justify-center bg-black rounded-lg">
                    <div class="text-center">
                        <i class="fas fa-film text-5xl text-secondary mb-4"></i>
                        <p class="text-white text-xl">预告片即将播放</p>
                        <p class="text-gray-400 mt-2">正在加载中...</p>
                    </div>
                </div>`;
                
                trailerModal.style.display = 'block';
                setTimeout(() => trailerModal.classList.add('active'), 10);
                document.body.style.overflow = 'hidden';
            }
        }
        
        function closeTrailerModal() {
            trailerModal.classList.remove('active');
            setTimeout(() => {
                trailerModal.style.display = 'none';
            }, 300);
            document.body.style.overflow = 'auto';
        }
    </script>
</body>
</html>
