



<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ملف التخزين</title>
    <script>
        function decodeAndStoreData() {
            // رابط الصفحة الحالية
            const currentURL = window.location.href;
            
            // الجزء المشفر من الرابط
            const encodedData = currentURL.split('?data=')[1];
            
            // فك تشفير البيانات
            const decodedData = decodeURIComponent(encodedData);
            const userData = JSON.parse(decodedData);
            
            // Access Token الخاص بك
            const accessToken = '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';
            
            // اسم المستودع ومسار الملف على GitHub
            const repo = ' ..github.io';
            const filePath = 'README.md';
            
            // رابط API لحفظ الملف
            const apiURL = `https://api.github.com/repos/${repo}/contents/${filePath}`;
            
            // البيانات التي سيتم حفظها في الملف
            const fileContent = JSON.stringify(userData);
            
            // طلب HTTP لحفظ الملف باستخدام Access Token
            fetch(apiURL, {
                method: 'PUT',
                headers: {
                    Authorization: `token ${accessToken}`,
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    message: 'تحديث بيانات المستخدم',
                    content: btoa(unescape(encodeURIComponent(fileContent))),
                    sha: null
                })
            })
            .then(response => {
                if (response.ok) {
                    alert('تم حفظ البيانات بنجاح!');
                } else {
                    alert('حدث خطأ أثناء حفظ البيانات.');
                }
            })
            .catch(error => {
                console.error('حدث خطأ:', error);
                alert('حدث خطأ أثناء حفظ البيانات.');
            });
        }
        
        decodeAndStoreData();
    </script>
</head>
<body>
    <p>جاري حفظ البيانات...</p>
</body>
</html>
