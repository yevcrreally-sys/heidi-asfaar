```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Heidi's Asfaar | هايدي أسفار</title>
    <!-- تحميل مكتبة Tailwind CSS للتصميم السريع والمتجاوب -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- تحميل خط Cairo العربي العصري والمميز -->
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    <!-- تحميل FontAwesome للأيقونات الفاخرة -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        gold: {
                            light: '#f5d77f',
                            DEFAULT: '#d4af37',
                            dark: '#aa820a',
                        },
                        darkBg: '#0b0b0b',
                        cardBg: '#141414',
                        cardBorder: '#262626'
                    },
                    fontFamily: {
                        cairo: ['Cairo', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        body {
            font-family: 'Cairo', sans-serif;
            background-color: #0b0b0b;
            color: #f3f4f6;
        }
        /* تأثيرات إضاءة وتوهج ذهبي فاخر */
        .gold-glow {
            box-shadow: 0 0 25px rgba(212, 175, 55, 0.15);
        }
        .gold-border {
            border: 1px solid rgba(212, 175, 55, 0.3);
        }
        .gold-border:focus {
            border-color: #d4af37;
            box-shadow: 0 0 10px rgba(212, 175, 55, 0.3);
        }
        /* تخصيص شريط التمرير */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0b0b0b;
        }
        ::-webkit-scrollbar-thumb {
            background: #333;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #d4af37;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between selection:bg-gold selection:text-black">

    <!-- حاوية التطبيق العامة -->
    <div class="max-w-md mx-auto w-full px-4 py-8 flex-grow flex flex-col items-center">

        <!-- الهيدر والشعار (مطابق للتصميم الراقي) -->
        <header class="text-center mb-8 w-full">
            <div class="relative w-28 h-28 mx-auto mb-4 rounded-full p-1 gold-border gold-glow bg-gradient-to-b from-cardBg to-black flex items-center justify-center">
                <!-- إمكانية تعديل الشعار أو وضع صورة الشعار الخاصة بك هنا -->
                <div class="text-gold text-3xl font-extrabold tracking-widest flex flex-col items-center">
                    <i class="fa-solid fa-crown text-2xl mb-1 text-gold"></i>
                    <span class="text-2xl font-black">HA</span>
                </div>
            </div>
            <h1 class="text-2xl md:text-3xl font-extrabold text-gold tracking-wide mb-2" dir="ltr">Heidi's Asfaar</h1>
            <p class="text-gray-400 text-sm font-light">نتعلم ونستفيد تحت نور شريعتنا وعلمنا</p>
        </header>

        <!-- منطقة التنبيهات المخصصة بدلاً من alert -->
        <div id="toast" class="hidden fixed top-5 left-1/2 transform -translate-x-1/2 z-50 bg-cardBg gold-border text-gold px-6 py-3 rounded-xl shadow-2xl text-sm flex items-center gap-3 transition-all duration-300">
            <i id="toast-icon" class="fa-solid fa-circle-check text-lg"></i>
            <span id="toast-message">تمت العملية بنجاح!</span>
        </div>

        <!-- 1. الواجهة الأولى: الرئيسية والتعريفية (Bio & Intro) -->
        <section id="view-home" class="w-full space-y-5 animate-fadeIn">
            
            <!-- صندوق النبذة التعريفية (قابل للتعديل أو العرض) -->
            <div class="bg-cardBg gold-border rounded-2xl p-5 shadow-xl relative group">
                <div class="flex justify-between items-center mb-2">
                    <span class="text-xs text-gold uppercase tracking-wider font-bold"><i class="fa-solid fa-circle-info ml-1"></i> نبذة تعريفية</span>
                    <!-- زر تبديل وضع التعديل للنص التعريفي -->
                    <button onclick="toggleEditBio()" class="text-gray-400 hover:text-gold text-xs transition">
                        <i class="fa-solid fa-pen-to-square"></i> تعديل
                    </button>
                </div>
                <p id="bio-text" class="text-gray-300 text-sm leading-relaxed font-light">
                    أهلاً بكِ في مساحتي الشخصية. هنا أشارك معكِ أحدث الأبحاث العلمية، المقالات الهادفة، وجداول المعرفة المفيدة المستمدة من Notion ومصادر موثوقة. يسعدني دائماً استقبال آرائكم وأسئلتكم!
                </p>
                <!-- حقل تعديل النبذة مخفي افتراضياً -->
                <div id="bio-edit-box" class="hidden mt-3">
                    <textarea id="bio-input" class="w-full bg-black/50 text-white text-sm p-3 rounded-xl gold-border focus:outline-none resize-none h-24" placeholder="اكتب نبذة تعريفية جديدة هنا..."></textarea>
                    <button onclick="saveBio()" class="mt-2 bg-gradient-to-r from-gold to-gold-dark text-black font-bold text-xs px-4 py-2 rounded-lg shadow hover:opacity-90 transition">حفظ التعديل</button>
                </div>
            </div>

            <!-- أزرار التنقل السريعة الفاخرة -->
            <div class="space-y-3">
                <button onclick="switchView('message')" class="w-full bg-gradient-to-r from-gold-dark via-gold to-gold-light text-black font-bold py-3.5 px-6 rounded-xl shadow-lg hover:shadow-gold/20 flex items-center justify-center gap-3 transition-all transform active:scale-95">
                    <i class="fa-solid fa-paper-plane text-lg"></i>
                    <span>إرسال سؤال أو رأي (للبريد مباشرة)</span>
                </button>

                <button onclick="switchView('library')" class="w-full bg-cardBg hover:bg-neutral-900 text-gold gold-border font-semibold py-3.5 px-6 rounded-xl shadow-md flex items-center justify-center gap-3 transition-all transform active:scale-95">
                    <i class="fa-solid fa-book-bookmark text-lg"></i>
                    <span>المكتبة ومصادر Notion & Drive</span>
                </button>

                <button onclick="switchView('links')" class="w-full bg-cardBg hover:bg-neutral-900 text-gray-200 gold-border font-semibold py-3.5 px-6 rounded-xl shadow-md flex items-center justify-center gap-3 transition-all transform active:scale-95">
                    <i class="fa-solid fa-share-nodes text-lg text-gold"></i>
                    <span>روابط حساباتي وقنواتي</span>
                </button>
            </div>

            <!-- قسم الردود المنشورة أو الإدارة التجريبية -->
            <div class="grid grid-cols-2 gap-3 pt-2">
                <button onclick="showToast('قسم الردود والمقالات قيد التحديث المستمر.', 'info')" class="bg-cardBg hover:bg-neutral-900 text-gray-400 hover:text-gold text-xs py-3 px-4 rounded-xl gold-border transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-comments"></i> الردود المنشورة
                </button>
                <button onclick="showToast('منطقة الإدارة مخصصة لمالكة الموقع.', 'info')" class="bg-cardBg hover:bg-neutral-900 text-gray-400 hover:text-gold text-xs py-3 px-4 rounded-xl gold-border transition flex items-center justify-center gap-2">
                    <i class="fa-solid fa-lock"></i> لوحة التحكم
                </button>
            </div>
        </section>


        <!-- 2. واجهة إرسال الرسائل والأسئلة (متصلة بالبريد الحقيقي عبر Web3Forms) -->
        <section id="view-message" class="w-full space-y-4 hidden animate-fadeIn">
            <div class="flex items-center justify-between mb-2">
                <button onclick="switchView('home')" class="text-gold text-sm flex items-center gap-2 hover:underline">
                    <i class="fa-solid fa-arrow-right"></i> العودة للرئيسية
                </button>
                <h2 class="text-gold font-bold text-base">مساحة المشاركة الآمنة</h2>
            </div>

            <!-- تنبيه إرشادي للمستخدمة حول كيفية ربط بريدها -->
            <div class="bg-neutral-900/80 gold-border p-4 rounded-xl text-xs text-gray-300 leading-relaxed">
                <p class="font-bold text-gold mb-1"><i class="fa-solid fa-lightbulb ml-1"></i> ملاحظة لمالكة الموقع (هايدي):</p>
                لاستقبال الرسائل على بريدك الإلكتروني الحقيقي فوراً، استبدلي القيمة في خاصية <code class="text-gold bg-black px-1 rounded">value</code> أدناه لمفتاحك المجاني من موقع <b>Web3Forms.com</b> (احصلي عليه بمجرد إدخال بريدك هناك مجاناً).
            </div>

            <!-- نموذج الإرسال الحقيقي -->
            <form action="https://api.web3forms.com/submit" method="POST" id="contact-form" class="bg-cardBg gold-border rounded-2xl p-5 space-y-4 shadow-xl">
                
                <!-- مفتاح الوصول المجاني لاستقبال البريد (يمكنك استبداله بمفتاحك الخاص) -->
                <input type="hidden" name="access_key" value="YOUR_ACCESS_KEY_HERE">
                <input type="hidden" name="subject" value="رسالة جديدة من زائر عبر موقع هايدي التفاعلي">

                <div>
                    <label class="block text-xs text-gray-400 mb-1.5 font-semibold">الاسم المستعار (اختياري)</label>
                    <input type="text" name="name" class="w-full bg-black/60 gold-border rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none" placeholder="اكتب اسمك أو اتركها فارغة...">
                </div>

                <div>
                    <label class="block text-xs text-gray-400 mb-1.5 font-semibold">نوع المشاركة</label>
                    <select name="type" class="w-full bg-black/60 gold-border rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none">
                        <option value="سؤال علمي">سؤال علمي أو شرعي</option>
                        <option value="رأي أو مقترح">رأي أو مقترح تطويري</option>
                        <option value="استفسار عام">استفسار عام</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs text-gray-400 mb-1.5 font-semibold">المجال</label>
                    <select name="field" class="w-full bg-black/60 gold-border rounded-xl px-4 py-2.5 text-sm text-white focus:outline-none">
                        <option value="عام">عام</option>
                        <option value="بحوث ودراسات">بحوث ودراسات</option>
                        <option value="العادات الصحية والاستيقاظ">العادات الصحية والاستيقاظ</option>
                        <option value="تطوير اللغة الإنجليزية">تطوير اللغة الإنجليزية</option>
                    </select>
                </div>

                <div>
                    <label class="block text-xs text-gray-400 mb-1.5 font-semibold">نَص المشاركة</label>
                    <textarea name="message" required rows="4" class="w-full bg-black/60 gold-border rounded-xl p-3 text-sm text-white focus:outline-none resize-none" placeholder="اكتب سؤالك أو رأيك باحترام، دون بيانات حساسة..."></textarea>
                </div>

                <div class="flex items-center gap-2 text-xs text-gray-400">
                    <input type="checkbox" id="allow-publish" class="accent-gold rounded">
                    <label for="allow-publish">أسمح بنشر مشاركتي مع الاسم المستعار والرد عليها.</label>
                </div>

                <button type="submit" class="w-full bg-gradient-to-r from-gold-dark via-gold to-gold-light text-black font-bold py-3 px-6 rounded-xl shadow-lg hover:opacity-90 transition transform active:scale-95 flex items-center justify-center gap-2">
                    <i class="fa-solid fa-paper-plane"></i> إرسال المشاركة للبريد
                </button>
            </form>
        </section>


        <!-- 3. واجهة "المكتبة والمصادر المنظمة" (Notion, Google Drive, الكتب والبحوث) -->
        <section id="view-library" class="w-full space-y-4 hidden animate-fadeIn">
            <div class="flex items-center justify-between mb-2">
                <button onclick="switchView('home')" class="text-gold text-sm flex items-center gap-2 hover:underline">
                    <i class="fa-solid fa-arrow-right"></i> العودة للرئيسية
                </button>
                <h2 class="text-gold font-bold text-base">المكتبة ومصادر المعرفة</h2>
            </div>

            <p class="text-xs text-gray-400 font-light mb-3">مكتبة منظمة تضم أهم جداول البحوث، الكتب الإلكترونية، وصفحات Notion التعليمية والدرايف.</p>

            <!-- حاوية البطاقات والمكتبة -->
            <div class="space-y-3">
                
                <!-- عنصر مكتبة 1: Notion -->
                <div class="bg-cardBg gold-border rounded-2xl p-4 hover:border-gold transition flex items-center justify-between">
                    <div class="flex items-center gap-3.5">
                        <div class="w-10 h-10 rounded-xl bg-black gold-border flex items-center justify-center text-gold text-lg">
                            <i class="fa-solid fa-table-cells"></i>
                        </div>
                        <div>
                            <h3 class="text-sm font-bold text-white">جداول البحوث والدراسات (Notion)</h3>
                            <p class="text-xs text-gray-400 mt-0.5">تنظيم الأبحاث والمراجع العلمية بأسلوب احترافي.</p>
                        </div>
                    </div>
                    <!-- استبدل الرابط أدناه برابط صفحة Notion الخاصة بك -->
                    <a href="https://www.notion.so" target="_blank" class="bg-neutral-900 text-gold hover:bg-gold hover:text-black text-xs font-bold py-2 px-3.5 rounded-xl gold-border transition flex items-center gap-1.5">
                        <span>فتح</span> <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                    </a>
                </div>

                <!-- عنصر مكتبة 2: Google Drive الكتب الإلكترونية -->
                <div class="bg-cardBg gold-border rounded-2xl p-4 hover:border-gold transition flex items-center justify-between">
                    <div class="flex items-center gap-3.5">
                        <div class="w-10 h-10 rounded-xl bg-black gold-border flex items-center justify-center text-gold text-lg">
                            <i class="fa-solid fa-book"></i>
                        </div>
                        <div>
                            <h3 class="text-sm font-bold text-white">مكتبة الكتب الإلكترونية (Google Drive)</h3>
                            <p class="text-xs text-gray-400 mt-0.5">كتب ومؤلفات مفيدة في تطوير الذات والعلوم.</p>
                        </div>
                    </div>
                    <!-- استبدل الرابط أدناه برابط مجلد Google Drive الخاص بك -->
                    <a href="https://drive.google.com" target="_blank" class="bg-neutral-900 text-gold hover:bg-gold hover:text-black text-xs font-bold py-2 px-3.5 rounded-xl gold-border transition flex items-center gap-1.5">
                        <span>تحميل</span> <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                    </a>
                </div>

                <!-- عنصر مكتبة 3: مقالات بودكاست أسفار -->
                <div class="bg-cardBg gold-border rounded-2xl p-4 hover:border-gold transition flex items-center justify-between">
                    <div class="flex items-center gap-3.5">
                        <div class="w-10 h-10 rounded-xl bg-black gold-border flex items-center justify-center text-gold text-lg">
                            <i class="fa-solid fa-podcast"></i>
                        </div>
                        <div>
                            <h3 class="text-sm font-bold text-white">حلقات ومقالات بودكاست أسفار</h3>
                            <p class="text-xs text-gray-400 mt-0.5">استمع واقرأ أحدث الحلقات حول العادات والاستيقاظ.</p>
                        </div>
                    </div>
                    <!-- استبدل الرابط أدناه برابط مدونتك أو سبستاك -->
                    <a href="https://substack.com" target="_blank" class="bg-neutral-900 text-gold hover:bg-gold hover:text-black text-xs font-bold py-2 px-3.5 rounded-xl gold-border transition flex items-center gap-1.5">
                        <span>قراءة</span> <i class="fa-solid fa-arrow-up-right-from-square text-[10px]"></i>
                    </a>
                </div>

            </div>
        </section>


        <!-- 4. واجهة روابط التواصل الاجتماعي (Bio Links) -->
        <section id="view-links" class="w-full space-y-4 hidden animate-fadeIn">
            <div class="flex items-center justify-between mb-2">
                <button onclick="switchView('home')" class="text-gold text-sm flex items-center gap-2 hover:underline">
                    <i class="fa-solid fa-arrow-right"></i> العودة للرئيسية
                </button>
                <h2 class="text-gold font-bold text-base">روابط حساباتي وقنواتي</h2>
            </div>

            <p class="text-xs text-gray-400 font-light mb-3">تستطيعين تعديل وتحديث هذه الروابط مباشرة داخل الكود لتوجيه الزوار إلى حساباتك.</p>

            <div class="space-y-3">
                <!-- رابط القناة -->
                <a href="https://youtube.com" target="_blank" class="bg-cardBg hover:bg-neutral-900 gold-border p-4 rounded-xl flex items-center justify-between text-white transition group">
                    <div class="flex items-center gap-3">
                        <i class="fa-brands fa-youtube text-red-500 text-xl w-6 text-center"></i>
                        <span class="text-sm font-semibold group-hover:text-gold transition">قناة اليوتيوب (بودكاست أسفار)</span>
                    </div>
                    <i class="fa-solid fa-chevron-left text-xs text-gray-500"></i>
                </a>

                <!-- رابط الموقع أو المدونة -->
                <a href="https://blogger.com" target="_blank" class="bg-cardBg hover:bg-neutral-900 gold-border p-4 rounded-xl flex items-center justify-between text-white transition group">
                    <div class="flex items-center gap-3">
                        <i class="fa-solid fa-blog text-gold text-xl w-6 text-center"></i>
                        <span class="text-sm font-semibold group-hover:text-gold transition">مدونة بلوجر / المقالات</span>
                    </div>
                    <i class="fa-solid fa-chevron-left text-xs text-gray-500"></i>
                </a>

                <!-- رابط سبستاك -->
                <a href="https://substack.com" target="_blank" class="bg-cardBg hover:bg-neutral-900 gold-border p-4 rounded-xl flex items-center justify-between text-white transition group">
                    <div class="flex items-center gap-3">
                        <i class="fa-solid fa-pen-nib text-orange-400 text-xl w-6 text-center"></i>
                        <span class="text-sm font-semibold group-hover:text-gold transition">نشرة سبستاك البريدية</span>
                    </div>
                    <i class="fa-solid fa-chevron-left text-xs text-gray-500"></i>
                </a>
            </div>
        </section>

    </div>

    <!-- تذييل الصفحة الفاخر -->
    <footer class="w-full text-center py-6 border-t border-neutral-900 text-xs text-gray-500 font-light mt-8">
        <p>جميع الحقوق محفوظة © <span class="text-gold font-medium">هايدي</span> | تصميم وتطوير فاخر ومجاني</p>
    </footer>

    <!-- السكريبت البرمجي للتحكم بالواجهات والتنبيهات وحفظ النبذة -->
    <script>
        // دالة التنقل بين الواجهات بسلاسة
        function switchView(viewName) {
            const views = ['home', 'message', 'library', 'links'];
            views.forEach(v => {
                const el = document.getElementById(`view-${v}`);
                if (el) {
                    if (v === viewName) {
                        el.classList.remove('hidden');
                        window.scrollTo({ top: 0, behavior: 'smooth' });
                    } else {
                        el.classList.add('hidden');
                    }
                }
            });
        }

        // دالة عرض رسائل التنبيهات المخصصة (بدلاً من alert)
        function showToast(message, type = 'success') {
            const toast = document.getElementById('toast');
            const msgEl = document.getElementById('toast-message');
            const iconEl = document.getElementById('toast-icon');

            msgEl.textContent = message;
            if (type === 'success') {
                iconEl.className = 'fa-solid fa-circle-check text-gold text-lg';
            } else {
                iconEl.className = 'fa-solid fa-circle-info text-gold text-lg';
            }

            toast.classList.remove('hidden');
            setTimeout(() => {
                toast.classList.add('hidden');
            }, 3500);
        }

        // وظائف تعديل النبذة التعريفية محلياً
        function toggleEditBio() {
            const bioText = document.getElementById('bio-text');
            const bioEditBox = document.getElementById('bio-edit-box');
            const bioInput = document.getElementById('bio-input');

            if (bioEditBox.classList.contains('hidden')) {
                bioEditBox.classList.remove('hidden');
                bioInput.value = bioText.textContent.trim();
            } else {
                bioEditBox.classList.add('hidden');
            }
        }

        function saveBio() {
            const bioInput = document.getElementById('bio-input');
            const bioText = document.getElementById('bio-text');
            const bioEditBox = document.getElementById('bio-edit-box');

            if (bioInput.value.trim() !== '') {
                bioText.textContent = bioInput.value.trim();
                showToast('تم تحديث النبذة التعريفية بنجاح!');
            }
            bioEditBox.classList.add('hidden');
        }

        // معالجة نموذج إرسال الرسائل عبر Web3Forms وتأكيد الإرسال
        const form = document.getElementById('contact-form');
        form.addEventListener('submit', function(e) {
            // ملاحظة: إذا قمتِ بوضع مفتاحك الحقيقي في حقل access_key، سيتم الإرسال لبريدك مباشرة
            // هنا نعرض رسالة نجاح أنيقة للزائر بعد الإرسال
            showToast('تم إرسال رسالتك بنجاح، شكراً لتواصلكِ مع هايدي!');
        });
    </script>
</body>
</html>
```
