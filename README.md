<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>两弹一星 - 抉择与回响</title>
    <style>
        /* 基础重置与全局样式 */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "SimHei", "Microsoft YaHei", "STKaiti", serif;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #000;
            overflow: hidden;
        }

        /* 固定H5容器：640×1008 核心尺寸 */
        .h5-container {
            width: 640px;
            height: 1008px;
            position: relative;
            overflow: hidden;
            border: none;
        }

        /* 通用页面样式：深红色背景基色 */
        .page {
            width: 100%;
            height: 100%;
            display: none;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
            text-align: center;
            background: linear-gradient(135deg, #8b0000, #4a0000); /* 深红色渐变主背景 */
            position: absolute;
            top: 0;
            left: 0;
        }

        /* 1. 加载页样式 - 背景图1 */
        #loading-page {
            display: flex;
            background: url(背景图1.jpg) no-repeat center center;
            background-size: cover; /* 背景图覆盖整个页面 */
        }

        .loading-title {
            font-size: 42px;
            color: #ffd700; /* 金色字体 */
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.9), 0 0 40px rgba(212, 175, 55, 0.7);
            margin-bottom: 20px;
            letter-spacing: 6px;
            font-weight: bold;
            font-family: "ZCOOL ChangHei", "STKaiti", cursive; /* 大气字体增强华丽感 */
        }

        .progress-container {
            width: 70%;
            height: 20px;
            background-color: #3a0000; /* 深红色进度条背景 */
            border-radius: 10px;
            margin-bottom: 20px;
            overflow: hidden;
            border: 2px solid #d4af37; /* 金色边框 */
            box-shadow: 0 0 15px rgba(212, 175, 55, 0.5);
        }

        .progress-bar {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, #d4af37, #ffd700, #f9f293); /* 金色渐变进度条 */
            border-radius: 8px;
            transition: width 2s ease-in-out; /* 进度条平滑过渡 */
            box-shadow: 0 0 10px rgba(255, 215, 0, 0.8);
        }

        .loading-subtitle {
            font-size: 28px;
            color: #f8ecc2; /* 浅金色字体 */
            text-shadow: 0 0 15px rgba(212, 175, 55, 0.7);
            letter-spacing: 4px;
            font-family: "ZCOOL ChangHei", "STKaiti", cursive;
        }

        /* 2. 两弹一星介绍页样式 */
        #intro-page {
            background: linear-gradient(135deg, #8b0000, #4a0000);
            padding: 40px;
        }

        .intro-content {
            max-width: 580px;
            margin-bottom: 80px;
            padding: 40px;
            background: rgba(0, 0, 0, 0.4); /* 半透明深色背景增强层次感 */
            border-radius: 15px;
            border: 2px solid #d4af37; /* 金色边框 */
            box-shadow: 0 0 25px rgba(212, 175, 55, 0.3);
        }

        .intro-title {
            font-size: 42px;
            color: #ffd700;
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.9);
            margin-bottom: 30px;
            letter-spacing: 5px;
            font-weight: bold;
            font-family: "ZCOOL ChangHei", "STKaiti", cursive;
        }

        .intro-text {
            font-size: 20px;
            line-height: 2;
            color: #f8ecc2;
            text-align: left;
            margin-bottom: 20px;
            text-shadow: 0 0 5px rgba(212, 175, 55, 0.3);
        }

        /* 星形按钮样式：华丽交互效果 */
        .star-btn {
            width: 90px;
            height: 90px;
            background: linear-gradient(135deg, #d4af37, #ffd700); /* 金色渐变 */
            clip-path: polygon(
                50% 0%,
                61% 35%,
                98% 35%,
                68% 57%,
                79% 91%,
                50% 70%,
                21% 91%,
                32% 57%,
                2% 35%,
                39% 35%
            );
            border: none;
            cursor: pointer;
            transition: all 0.4s ease;
            box-shadow: 0 0 25px rgba(255, 215, 0, 0.7), inset 0 0 10px rgba(100, 70, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 16px;
            color: #4a0000; /* 深红色文字 */
            font-weight: bold;
            letter-spacing: 1px;
        }

        .star-btn:hover {
            transform: scale(1.15) rotate(10deg);
            box-shadow: 0 0 35px rgba(255, 215, 0, 0.9), inset 0 0 15px rgba(100, 70, 0, 0.7);
            background: linear-gradient(135deg, #ffd700, #f9f293);
        }

        /* 视频页面样式 - 背景图2 */
        .video-page {
            background: url(背景图2.jpg) no-repeat center center;
            background-size: cover;
            justify-content: center; /* 视频居中显示 */
            align-items: center;
            padding: 0; /* 移除内边距，最大化视频空间 */
        }

        /* 视频容器：无边框、全屏占比、无遮挡【核心优化】 */
        .video-container {
            width: 98%; /* 几乎占满页面宽度 */
            height: 90%; /* 大幅提升高度占比 */
            position: relative;
            border: none; /* 彻底移除边框 */
            border-radius: 0;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
            /* 移除半透明背景框，解决不美观问题 */
            background: transparent;
            box-shadow: none; /* 移除阴影，避免多余装饰 */
        }

        video {
            width: 100%;
            height: 100%;
            object-fit: contain; /* 保持视频比例，全屏显示不裁剪 */
            border: none; /* 确保视频自身无边框 */
            outline: none; /* 移除焦点轮廓 */
        }

        /* 选项页面样式 */
        .options-page {
            background: linear-gradient(135deg, #8b0000, #4a0000);
        }

        .options-title {
            font-size: 36px;
            color: #ffd700;
            text-shadow: 0 0 20px rgba(255, 215, 0, 0.8);
            margin-bottom: 60px;
            padding: 20px 40px;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 15px;
            border: 2px solid #d4af37;
            letter-spacing: 3px;
            font-family: "ZCOOL ChangHei", "STKaiti", cursive;
            box-shadow: 0 0 20px rgba(212, 175, 55, 0.3);
        }

        .options-container {
            display: flex;
            flex-direction: column;
            gap: 35px;
            width: 85%;
        }

        /* 选项按钮样式：华丽交互 */
        .option-btn {
            padding: 25px 40px;
            background: linear-gradient(135deg, #5a0000, #3a0000); /* 深红色渐变 */
            color: #f8ecc2;
            border: 3px solid #d4af37; /* 金色边框 */
            border-radius: 12px;
            font-size: 22px;
            cursor: pointer;
            transition: all 0.4s ease;
            text-align: center;
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.4), inset 0 0 10px rgba(212, 175, 55, 0.1);
            letter-spacing: 2px;
            font-family: "SimHei", "Microsoft YaHei", serif;
        }

        .option-btn:hover {
            background: linear-gradient(135deg, #d4af37, #ffd700); /* 金色渐变hover */
            color: #3a0000;
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5), inset 0 0 15px rgba(100, 70, 0, 0.3);
        }

        /* 感谢页样式 */
        #thanks-page {
            background: linear-gradient(135deg, #8b0000, #4a0000);
        }

        .thanks-text {
            font-size: 64px;
            color: #ffd700;
            text-shadow: 0 0 30px rgba(255, 215, 0, 0.9), 0 0 60px rgba(212, 175, 55, 0.7);
            animation: fadeInScale 2s ease-in-out;
            font-weight: bold;
            letter-spacing: 8px;
            font-family: "ZCOOL ChangHei", "STKaiti", cursive;
        }

        @keyframes fadeInScale {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }

        /* 适配小屏幕（保持640×1008比例） */
        @media (max-width: 640px) {
            .h5-container {
                width: 100vw;
                height: calc(100vw * 1008 / 640);
            }

            .video-container {
                width: 98%;
                height: 90%; /* 小屏幕保持高占比 */
            }

            .options-title {
                font-size: 28px;
            }

            .option-btn {
                font-size: 18px;
            }

            .thanks-text {
                font-size: 48px;
            }
        }
    </style>
    <!-- 引入大气字体增强华丽感（站酷畅言体） -->
    <link href="https://fonts.googleapis.com/css2?family=ZCOOL+ChangHei&display=swap" rel="stylesheet">
</head>
<body>
    <!-- 固定尺寸H5容器 -->
    <div class="h5-container">
        <!-- 1. 加载页 -->
        <div id="loading-page" class="page">
            <div class="loading-title">抉择 回响</div>
            <div class="progress-container">
                <div id="progress-bar" class="progress-bar"></div>
            </div>
            <div class="loading-subtitle">我的“两弹一星”</div>
        </div>

        <!-- 2. 两弹一星介绍页 -->
        <div id="intro-page" class="page">
            <div class="intro-content">
                <h1 class="intro-title">两弹一星</h1>
                <p class="intro-text">“两弹一星”最初指原子弹、氢弹、人造卫星，后“两弹”合指核弹与导弹，“一星”即人造地球卫星。</p>
                <p class="intro-text">20世纪50至70年代，中国科研工作者在极端艰苦的条件下，自力更生、艰苦奋斗，成功研制出“两弹一星”，打破了超级大国的核垄断，奠定了中国在国际上的重要地位。</p>
            </div>
            <button id="enter-history-btn" class="star-btn">进入</button>
        </div>

        <!-- 3. 视频页：开幕 -->
        <div id="video1-page" class="page video-page">
            <div class="video-container">
                <video id="video1" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/%E5%BC%80%E5%B9%95.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 4. 视频页：受命 -->
        <div id="video2-page" class="page video-page">
            <div class="video-container">
                <video id="video2" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/%E5%8F%97%E5%91%BD.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 5. 选项页：接受/拒绝 -->
        <div id="option1-page" class="page options-page">
            <h2 class="options-title">是否接受这项艰巨的任务？</h2>
            <div class="options-container">
                <button id="accept-btn" class="option-btn">接受</button>
                <button id="refuse-btn" class="option-btn">拒绝</button>
            </div>
        </div>

        <!-- 6. 视频页：2-1（接受后） -->
        <div id="video3-page" class="page video-page">
            <div class="video-container">
                <video id="video3" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/2-1.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 7. 视频页：2-2（拒绝后） -->
        <div id="video-refuse-page" class="page video-page">
            <div class="video-container">
                <video id="video-refuse" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/2-2.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 8. 选项页：回到当初（拒绝视频后） -->
        <div id="option-back-page" class="page options-page">
            <h2 class="options-title">如果时光倒流，你是否会重新选择？</h2>
            <div class="options-container">
                <button id="back-btn" class="option-btn">回到当初</button>
            </div>
        </div>

        <!-- 9. 选项页：钻研（2-1视频后） -->
        <div id="option2-page" class="page options-page">
            <h2 class="options-title">面对技术难题，你选择？</h2>
            <div class="options-container">
                <button id="research-btn" class="option-btn">钻研</button>
            </div>
        </div>

        <!-- 10. 视频页：3-1（钻研后） -->
        <div id="video4-page" class="page video-page">
            <div class="video-container">
                <video id="video4" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/3-1.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 11. 选项页：三个选择（3-1视频后） -->
        <div id="option3-page" class="page options-page">
            <h2 class="options-title">解决核心计算问题，你认为？</h2>
            <div class="options-container">
                <button id="option-a" class="option-btn">科学需要协作，我们必须携手攻关</button>
                <button id="option-b" class="option-btn">这......这真的可能吗？</button>
                <button id="option-c" class="option-btn">一人不行就上百，用算盘也要算出来</button>
            </div>
        </div>

        <!-- 12. 视频页：3-1-A -->
        <div id="video5-page" class="page video-page">
            <div class="video-container">
                <video id="video5" autoplay playsinline controls>
                    <source srchttps://justaworkplace.oss-cn-beijing.aliyuncs.com/3-1-A.mp43-1-A.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 13. 视频页：3-1-B -->
        <div id="video6-page" class="page video-page">
            <div class="video-container">
                <video id="video6" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/3-1-B.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 14. 视频页：3-1-C -->
        <div id="video7-page" class="page video-page">
            <div class="video-container">
                <video id="video7" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/3-1-C.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 15. 视频页：3-2 -->
        <div id="video8-page" class="page video-page">
            <div class="video-container">
                <video id="video8" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/3-2.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 16. 视频页：4-1 -->
        <div id="video9-page" class="page video-page">
            <div class="video-container">
                <video id="video9" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/4-1.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 17. 选项页：三个情感选项（4-1视频后） -->
        <div id="option4-page" class="page options-page">
            <h2 class="options-title">见证这一时刻，你想说？</h2>
            <div class="options-container">
                <button id="option-d" class="option-btn">默默致敬 这太不容易了......</button>
                <button id="option-e" class="option-btn">我们成功了！</button>
                <button id="option-f" class="option-btn">为了祖国，一切都值得</button>
            </div>
        </div>

        <!-- 18. 视频页：4-2 -->
        <div id="video10-page" class="page video-page">
            <div class="video-container">
                <video id="video10" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/4-2.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 19. 视频页：奉献 -->
        <div id="video11-page" class="page video-page">
            <div class="video-container">
                <video id="video11" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/%E5%A5%89%E7%8C%AE.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 20. 选项页：看彩蛋/不看彩蛋 -->
        <div id="option5-page" class="page options-page">
            <h2 class="options-title">是否查看彩蛋？</h2>
            <div class="options-container">
                <button id="egg-btn" class="option-btn">看彩蛋</button>
                <button id="no-egg-btn" class="option-btn">不看彩蛋</button>
            </div>
        </div>

        <!-- 21. 视频页：结尾彩蛋 -->
        <div id="video-egg-page" class="page video-page">
            <div class="video-container">
                <video id="video-egg" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/%E7%BB%93%E5%B0%BE%E5%BD%A9%E8%9B%8B.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 22. 视频页：结尾 无彩蛋 -->
        <div id="video-no-egg-page" class="page video-page">
            <div class="video-container">
                <video id="video-no-egg" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/%E7%BB%93%E5%B0%BE%20%E6%97%A0%E5%BD%A9%E8%9B%8B.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 23. 视频页：最终结尾 -->
        <div id="video-final-page" class="page video-page">
            <div class="video-container">
                <video id="video-final" autoplay playsinline controls>
                    <source src="https://justaworkplace.oss-cn-beijing.aliyuncs.com/%E6%9C%80%E7%BB%88%E7%BB%93%E5%B0%BE.mp4" type="video/mp4">
                    您的浏览器不支持视频播放
                </video>
            </div>
        </div>

        <!-- 24. 感谢页 -->
        <div id="thanks-page" class="page">
            <div class="thanks-text">谢谢观看</div>
        </div>
    </div>

    <script>
        // ========== DOM元素获取 ==========
        // 加载页
        const loadingPage = document.getElementById('loading-page');
        const progressBar = document.getElementById('progress-bar');
        // 介绍页
        const introPage = document.getElementById('intro-page');
        const enterHistoryBtn = document.getElementById('enter-history-btn');
        // 视频页1-开幕
        const video1Page = document.getElementById('video1-page');
        const video1 = document.getElementById('video1');
        // 视频页2-受命
        const video2Page = document.getElementById('video2-page');
        const video2 = document.getElementById('video2');
        // 选项页1-接受/拒绝
        const option1Page = document.getElementById('option1-page');
        const acceptBtn = document.getElementById('accept-btn');
        const refuseBtn = document.getElementById('refuse-btn');
        // 视频页3-2-1
        const video3Page = document.getElementById('video3-page');
        const video3 = document.getElementById('video3');
        // 视频页-拒绝后2-2
        const videoRefusePage = document.getElementById('video-refuse-page');
        const videoRefuse = document.getElementById('video-refuse');
        // 选项页-回到当初
        const optionBackPage = document.getElementById('option-back-page');
        const backBtn = document.getElementById('back-btn');
        // 选项页2-钻研
        const option2Page = document.getElementById('option2-page');
        const researchBtn = document.getElementById('research-btn');
        // 视频页4-3-1
        const video4Page = document.getElementById('video4-page');
        const video4 = document.getElementById('video4');
        // 选项页3-三个选择
        const option3Page = document.getElementById('option3-page');
        const optionA = document.getElementById('option-a');
        const optionB = document.getElementById('option-b');
        const optionC = document.getElementById('option-c');
        // 视频页5-3-1-A
        const video5Page = document.getElementById('video5-page');
        const video5 = document.getElementById('video5');
        // 视频页6-3-1-B
        const video6Page = document.getElementById('video6-page');
        const video6 = document.getElementById('video6');
        // 视频页7-3-1-C
        const video7Page = document.getElementById('video7-page');
        const video7 = document.getElementById('video7');
        // 视频页8-3-2
        const video8Page = document.getElementById('video8-page');
        const video8 = document.getElementById('video8');
        // 视频页9-4-1
        const video9Page = document.getElementById('video9-page');
        const video9 = document.getElementById('video9');
        // 选项页4-三个情感选项
        const option4Page = document.getElementById('option4-page');
        const optionD = document.getElementById('option-d');
        const optionE = document.getElementById('option-e');
        const optionF = document.getElementById('option-f');
        // 视频页10-4-2
        const video10Page = document.getElementById('video10-page');
        const video10 = document.getElementById('video10');
        // 视频页11-奉献
        const video11Page = document.getElementById('video11-page');
        const video11 = document.getElementById('video11');
        // 选项页5-彩蛋选择
        const option5Page = document.getElementById('option5-page');
        const eggBtn = document.getElementById('egg-btn');
        const noEggBtn = document.getElementById('no-egg-btn');
        // 视频页-彩蛋
        const videoEggPage = document.getElementById('video-egg-page');
        const videoEgg = document.getElementById('video-egg');
        // 视频页-无彩蛋
        const videoNoEggPage = document.getElementById('video-no-egg-page');
        const videoNoEgg = document.getElementById('video-no-egg');
        // 视频页-最终结尾
        const videoFinalPage = document.getElementById('video-final-page');
        const videoFinal = document.getElementById('video-final');
        // 感谢页
        const thanksPage = document.getElementById('thanks-page');

        // ========== 核心功能函数 ==========
        /**
         * 处理浏览器自动播放限制的通用函数
         * @param {HTMLVideoElement} videoElement - 视频元素
         * @param {HTMLElement} pageElement - 视频所在页面元素
         */
        function playVideoWithInteraction(videoElement, pageElement) {
            // 先尝试自动播放
            const playPromise = videoElement.play();
            if (playPromise !== undefined) {
                playPromise.catch(err => {
                    console.log('自动播放失败，等待用户交互：', err);
                    // 绑定点击事件触发播放（无提示，直接点击页面播放）
                    pageElement.addEventListener('click', () => {
                        videoElement.play();
                    }, { once: true });
                });
            }
        }

        // ========== 页面逻辑 ==========
        // 1. 模拟加载进度【核心修复：进度条必须满100%才进入页面】
        window.onload = function() {
            let progress = 0;
            const interval = setInterval(() => {
                progress += Math.random() * 15; // 减慢加载速度，确保进度条能满100%
                if (progress >= 100) {
                    progress = 100;
                    progressBar.style.width = progress + '%'; // 强制设置为100%
                    clearInterval(interval);
                    // 加载完成后延迟0.8秒进入介绍页（进度条完全满后再跳转）
                    setTimeout(() => {
                        loadingPage.style.display = 'none';
                        introPage.style.display = 'flex';
                    }, 800);
                } else {
                    progressBar.style.width = progress + '%';
                }
            }, 50);
        };

        // 2. 星形按钮：进入历史体验（跳转到开幕视频页）
        enterHistoryBtn.addEventListener('click', () => {
            introPage.style.display = 'none';
            video1Page.style.display = 'flex';
            playVideoWithInteraction(video1, video1Page);
        });

        // 3. 开幕视频播放完毕 → 受命视频页
        video1.addEventListener('ended', () => {
            video1Page.style.display = 'none';
            video2Page.style.display = 'flex';
            playVideoWithInteraction(video2, video2Page);
        });

        // 4. 受命视频播放完毕 → 接受/拒绝选项页
        video2.addEventListener('ended', () => {
            video2Page.style.display = 'none';
            option1Page.style.display = 'flex';
        });

        // 5. 接受按钮 → 2-1视频页
        acceptBtn.addEventListener('click', () => {
            option1Page.style.display = 'none';
            video3Page.style.display = 'flex';
            playVideoWithInteraction(video3, video3Page);
        });

        // 6. 拒绝按钮 → 2-2视频页
        refuseBtn.addEventListener('click', () => {
            option1Page.style.display = 'none';
            videoRefusePage.style.display = 'flex';
            playVideoWithInteraction(videoRefuse, videoRefusePage);
        });

        // 7. 2-2视频播放完毕 → 回到当初选项页
        videoRefuse.addEventListener('ended', () => {
            videoRefusePage.style.display = 'none';
            optionBackPage.style.display = 'flex';
        });

        // 8. 回到当初 → 受命视频页
        backBtn.addEventListener('click', () => {
            optionBackPage.style.display = 'none';
            video2Page.style.display = 'flex';
            playVideoWithInteraction(video2, video2Page);
        });

        // 9. 2-1视频播放完毕 → 钻研选项页
        video3.addEventListener('ended', () => {
            video3Page.style.display = 'none';
            option2Page.style.display = 'flex';
        });

        // 10. 钻研按钮 → 3-1视频页
        researchBtn.addEventListener('click', () => {
            option2Page.style.display = 'none';
            video4Page.style.display = 'flex';
            playVideoWithInteraction(video4, video4Page);
        });

        // 11. 3-1视频播放完毕 → 三个选择选项页
        video4.addEventListener('ended', () => {
            video4Page.style.display = 'none';
            option3Page.style.display = 'flex';
        });

        // 12. 选项A → 3-1-A视频页
        optionA.addEventListener('click', () => {
            option3Page.style.display = 'none';
            video5Page.style.display = 'flex';
            playVideoWithInteraction(video5, video5Page);
        });

        // 13. 选项B → 3-1-B视频页
        optionB.addEventListener('click', () => {
            option3Page.style.display = 'none';
            video6Page.style.display = 'flex';
            playVideoWithInteraction(video6, video6Page);
        });

        // 14. 选项C → 3-1-C视频页
        optionC.addEventListener('click', () => {
            option3Page.style.display = 'none';
            video7Page.style.display = 'flex';
            playVideoWithInteraction(video7, video7Page);
        });

        // 15. 3-1-A视频播放完毕 → 3-2视频页
        video5.addEventListener('ended', () => {
            video5Page.style.display = 'none';
            video8Page.style.display = 'flex';
            playVideoWithInteraction(video8, video8Page);
        });

        // 16. 3-1-B视频播放完毕 → 3-2视频页
        video6.addEventListener('ended', () => {
            video6Page.style.display = 'none';
            video8Page.style.display = 'flex';
            playVideoWithInteraction(video8, video8Page);
        });

        // 17. 3-1-C视频播放完毕 → 3-2视频页
        video7.addEventListener('ended', () => {
            video7Page.style.display = 'none';
            video8Page.style.display = 'flex';
            playVideoWithInteraction(video8, video8Page);
        });

        // 18. 3-2视频播放完毕 → 4-1视频页
        video8.addEventListener('ended', () => {
            video8Page.style.display = 'none';
            video9Page.style.display = 'flex';
            playVideoWithInteraction(video9, video9Page);
        });

        // 19. 4-1视频播放完毕 → 三个情感选项页
        video9.addEventListener('ended', () => {
            video9Page.style.display = 'none';
            option4Page.style.display = 'flex';
        });

        // 20. 情感选项D/E/F → 4-2视频页
        optionD.addEventListener('click', () => {
            option4Page.style.display = 'none';
            video10Page.style.display = 'flex';
            playVideoWithInteraction(video10, video10Page);
        });
        optionE.addEventListener('click', () => {
            option4Page.style.display = 'none';
            video10Page.style.display = 'flex';
            playVideoWithInteraction(video10, video10Page);
        });
        optionF.addEventListener('click', () => {
            option4Page.style.display = 'none';
            video10Page.style.display = 'flex';
            playVideoWithInteraction(video10, video10Page);
        });

        // 21. 4-2视频播放完毕 → 奉献视频页
        video10.addEventListener('ended', () => {
            video10Page.style.display = 'none';
            video11Page.style.display = 'flex';
            playVideoWithInteraction(video11, video11Page);
        });

        // 22. 奉献视频播放完毕 → 彩蛋选择页
        video11.addEventListener('ended', () => {
            video11Page.style.display = 'none';
            option5Page.style.display = 'flex';
        });

        // 23. 看彩蛋 → 结尾彩蛋视频页
        eggBtn.addEventListener('click', () => {
            option5Page.style.display = 'none';
            videoEggPage.style.display = 'flex';
            playVideoWithInteraction(videoEgg, videoEggPage);
        });

        // 24. 不看彩蛋 → 结尾无彩蛋视频页
        noEggBtn.addEventListener('click', () => {
            option5Page.style.display = 'none';
            videoNoEggPage.style.display = 'flex';
            playVideoWithInteraction(videoNoEgg, videoNoEggPage);
        });

        // 25. 结尾彩蛋视频播放完毕 → 最终结尾视频页
        videoEgg.addEventListener('ended', () => {
            videoEggPage.style.display = 'none';
            videoFinalPage.style.display = 'flex';
            playVideoWithInteraction(videoFinal, videoFinalPage);
        });

        // 26. 结尾无彩蛋视频播放完毕 → 最终结尾视频页
        videoNoEgg.addEventListener('ended', () => {
            videoNoEggPage.style.display = 'none';
            videoFinalPage.style.display = 'flex';
            playVideoWithInteraction(videoFinal, videoFinalPage);
        });

        // 27. 最终结尾视频播放完毕 → 感谢页
        videoFinal.addEventListener('ended', () => {
            videoFinalPage.style.display = 'none';
            thanksPage.style.display = 'flex';
        });
    </script>
</body>
</html>
