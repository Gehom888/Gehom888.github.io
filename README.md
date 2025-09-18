<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="referrer" content="no-referrer">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>创建意见箱</title>
    <!-- 引入Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- 引入Font Awesome -->
    <link href="/Gehom88/https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    
    <!-- 配置Tailwind自定义颜色 -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        primary: '#3B82F6',
                        secondary: '#6B7280',
                        accent: '#1E40AF',
                        light: '#F3F4F6',
                    },
                    fontFamily: {
                        sans: ['system-ui', 'sans-serif'],
                    },
                }
            }
        }
    </script>
    
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .input-focus {
                @apply focus:ring-2 focus:ring-primary/50 focus:border-primary focus:outline-none;
            }
            .upload-hover {
                @apply hover:border-primary hover:bg-primary/5 transition-all duration-300;
            }
        }
    </style>
</head>
<body class="bg-gray-50 font-sans text-gray-800 min-h-screen">
    <!-- 顶部导航栏 -->
    <header class="bg-primary text-white p-4 shadow-md">
        <div class="container mx-auto flex justify-between items-center">
            <button class="text-white focus:outline-none">
                
            </button>
            <h1 class="text-xl font-medium">游客创建意见箱</h1>
            <div class="flex space-x-4">
                <button class="text-white focus:outline-none">
                    
                </button>
                <button class="text-white focus:outline-none">
                    
                </button>
            </div>
        </div>
    </header>

    <!-- 主要内容区 -->
    <main class="container mx-auto p-4 max-w-md">
        <form id="suggestionForm" class="space-y-6 mt-2">
            <!-- 意见箱名称 -->
            <div>
                <label for="boxName" class="block text-sm text-gray-600 mb-1">请填写名称，如：xxx公司意见箱</label>
                <input 
                    type="text" 
                    id="boxName" 
                    class="w-full px-4 py-2 border border-gray-300 rounded-lg input-focus text-base"
                    placeholder="输入意见箱名称"
                >
            </div>

            <!-- 简要介绍 -->
            <div>
                <label for="description" class="block text-sm text-gray-600 mb-1">请留下您的投诉与反馈...</label>
                <textarea 
                    id="description" 
                    rows="4" 
                    class="w-full px-4 py-2 border border-gray-300 rounded-lg input-focus text-base resize-none"
                    placeholder="输入反馈"
                ></textarea>
            </div>

            <!-- 上传Logo -->
            <div>
                <label class="block text-sm text-gray-600 mb-1">上传意见箱Logo（建议尺寸：100*100px）</label>
                <div class="relative">
                    <div id="logoUploadArea" class="border-2 border-dashed border-gray-300 rounded-lg p-6 text-center upload-hover cursor-pointer">
                        <i class="fa fa-upload text-gray-400 text-2xl mb-2"></i>
                        <p class="text-gray-500 text-sm">点击上传图片</p>
                        <img id="logoPreview" class="hidden absolute inset-0 w-full h-full object-contain rounded-lg" alt="Logo预览">
                    </div>
                    <input 
                        type="file" 
                        id="logoUpload" 
                        accept="image/*" 
                        class="absolute inset-0 w-full h-full opacity-0 cursor-pointer"
                    >
                </div>
            </div>

            <!-- 上传背景图 -->
            <div>
                <label class="block text-sm text-gray-600 mb-1">上传意见箱背景图（建议尺寸：750*563px）</label>
                <div class="relative">
                    <div id="bgUploadArea" class="border-2 border-dashed border-gray-300 rounded-lg p-8 text-center upload-hover cursor-pointer">
                        <i class="fa fa-picture-o text-gray-400 text-2xl mb-2"></i>
                        <p class="text-gray-500 text-sm">点击上传背景图片</p>
                        <img id="bgPreview" class="hidden absolute inset-0 w-full h-full object-cover rounded-lg" alt="背景图预览">
                    </div>
                    <input 
                        type="file" 
                        id="bgUpload" 
                        accept="image/*" 
                        class="absolute inset-0 w-full h-full opacity-0 cursor-pointer"
                    >
                </div>
            </div>

            <!-- 采纳有奖 -->
            <div class="flex items-center">
                <input 
                    type="checkbox" 
                    id="reward" 
                    class="w-5 h-5 text-primary rounded border-gray-300 focus:ring-primary"
                >
                <label for="reward" class="ml-2 text-gray-700">采纳有奖</label>
            </div>

            <!-- 自定义收集项 -->

            <!-- 创建按钮 -->
            <button 
                type="submit" 
                class="w-full bg-primary hover:bg-accent text-white font-medium py-3 px-4 rounded-lg transition-colors duration-300 transform hover:scale-[1.02] active:scale-[0.98]"
            >
                创建意见箱
            </button>
        </form>
    </main>

    <script>
        // Logo上传和预览
        const logoUpload = document.getElementById('logoUpload');
        const logoPreview = document.getElementById('logoPreview');
        const logoUploadArea = document.getElementById('logoUploadArea');

        logoUpload.addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(event) {
                    logoPreview.src = event.target.result;
                    logoPreview.classList.remove('hidden');
                    logoUploadArea.classList.add('border-primary');
                };
                reader.readAsDataURL(file);
            }
        });

        // 点击上传区域触发文件选择
        logoUploadArea.addEventListener('click', function() {
            logoUpload.click();
        });

        // 背景图上传和预览
        const bgUpload = document.getElementById('bgUpload');
        const bgPreview = document.getElementById('bgPreview');
        const bgUploadArea = document.getElementById('bgUploadArea');

        bgUpload.addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(event) {
                    bgPreview.src = event.target.result;
                    bgPreview.classList.remove('hidden');
                    bgUploadArea.classList.add('border-primary');
                };
                reader.readAsDataURL(file);
            }
        });

        // 点击上传区域触发文件选择
        bgUploadArea.addEventListener('click', function() {
            bgUpload.click();
        });

        // 填写示例按钮功能
        document.querySelector('button:text-primary').addEventListener('click', function() {
            document.getElementById('description').value = '希望全体员工积极建言献策，共同助力公司的发展与进步，您的每一条建议都将被认真对待。';
        });

        // 表单提交处理
        document.getElementById('suggestionForm').addEventListener('submit', function(e) {
            e.preventDefault();
            
            // 简单验证
            const boxName = document.getElementById('boxName').value;
            if (!boxName.trim()) {
                alert('请填写意见箱名称');
                return;
            }
            
            // 模拟提交成功
            alert('意见箱创建成功！');
            
            // 重置表单
            this.reset();
            logoPreview.classList.add('hidden');
            bgPreview.classList.add('hidden');
            logoUploadArea.classList.remove('border-primary');
            bgUploadArea.classList.remove('border-primary');
        });
    </script>
</body>
</html>
