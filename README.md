<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>בוט חיפוש רכבים להשכרה</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        .hidden {
            display: none;
        }
        @keyframes spin {
            to { transform: rotate(360deg); }
        }
        .animate-spin {
            animation: spin 1s linear infinite;
        }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 via-white to-purple-50 min-h-screen">
    <div class="max-w-6xl mx-auto p-6">
        <div class="text-center mb-8">
            <div class="flex items-center justify-center gap-3 mb-4">
                <svg class="w-12 h-12 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"></path>
                </svg>
                <h1 class="text-4xl font-bold text-gray-800">בוט חיפוש רכבים להשכרה</h1>
            </div>
            <p class="text-gray-600">מצא את הרכב הכי זול בקלות - השוואת מחירים אוטומטית</p>
        </div>

        <div class="flex gap-2 mb-6">
            <button onclick="switchTab('search')" id="tab-search" class="flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-blue-600 text-white shadow-lg">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                </svg>
                חיפוש חדש
            </button>
            <button onclick="switchTab('results')" id="tab-results" class="flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-white text-gray-600 hover:bg-gray-50">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"></path>
                </svg>
                תוצאות (<span id="results-count">0</span>)
            </button>
            <button onclick="switchTab('history')" id="tab-history" class="flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-white text-gray-600 hover:bg-gray-50">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                היסטוריה (<span id="history-count">0</span>)
            </button>
        </div>

        <div id="search-section" class="bg-white rounded-2xl shadow-xl p-8 mb-6">
            <div class="grid md:grid-cols-2 gap-6 mb-6">
                <div>
                    <label class="flex items-center gap-2 text-gray-700 font-semibold mb-2">
                        <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                        </svg>
                        תאריך איסוף
                    </label>
                    <input type="date" id="pickup-date" class="w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors">
                </div>
                
                <div>
                    <label class="flex items-center gap-2 text-gray-700 font-semibold mb-2">
                        <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z"></path>
                        </svg>
                        תאריך החזרה
                    </label>
                    <input type="date" id="return-date" class="w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors">
                </div>
            </div>

            <div class="mb-6">
                <label class="flex items-center gap-2 text-gray-700 font-semibold mb-2">
                    <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path>
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path>
                    </svg>
                    מיקום איסוף
                </label>
                <input type="text" id="location" placeholder="למשל: נתב״ג, תל אביב, ירושלים..." class="w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors">
            </div>

            <div class="mb-6">
                <label class="flex items-center gap-2 text-gray-700 font-semibold mb-2">
                    <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 7h.01M7 3h5c.512 0 1.024.195 1.414.586l7 7a2 2 0 010 2.828l-7 7a2 2 0 01-2.828 0l-7-7A1.994 1.994 0 013 12V7a4 4 0 014-4z"></path>
                    </svg>
                    קוד הנחה (אופציונלי)
                </label>
                <input type="text" id="promo-code" placeholder="הזן קוד הנחה..." class="w-full px-4 py-3 border-2 border-gray-200 rounded-lg focus:border-blue-500 focus:outline-none transition-colors">
            </div>

            <button onclick="handleSearch()" class="w-full bg-gradient-to-r from-blue-600 to-purple-600 text-white py-4 rounded-lg font-bold text-lg hover:from-blue-700 hover:to-purple-700 transition-all shadow-lg hover:shadow-xl flex items-center justify-center gap-2">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"></path>
                </svg>
                חפש רכבים זמינים
            </button>

            <div class="mt-6 p-4 bg-blue-50 rounded-lg">
                <p class="text-sm text-blue-800">
                    💡 <strong>טיפ:</strong> הבוט משווה מחירים מ-8 חברות השכרה מובילות בישראל ומציג לך את העסקה הכי משתלמת!
                </p>
            </div>
        </div>

        <div id="results-section" class="hidden">
            <div id="loading-spinner" class="hidden bg-white rounded-2xl shadow-xl p-12 text-center">
                <div class="animate-spin rounded-full h-16 w-16 border-b-4 border-blue-600 mx-auto mb-4"></div>
                <p class="text-xl text-gray-600">סורק את כל חברות ההשכרה...</p>
            </div>
            <div id="results-list" class="space-y-4"></div>
            <div id="no-results" class="hidden bg-white rounded-2xl shadow-xl p-12 text-center">
                <svg class="w-16 h-16 text-gray-300 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7h12m0 0l-4-4m4 4l-4 4m0 6H4m0 0l4 4m-4-4l4-4"></path>
                </svg>
                <p class="text-xl text-gray-600">עדיין לא חיפשת. לך ללשונית "חיפוש חדש" כדי להתחיל!</p>
            </div>
        </div>

        <div id="history-section" class="hidden">
            <div id="history-list" class="space-y-4"></div>
            <div id="no-history" class="bg-white rounded-2xl shadow-xl p-12 text-center">
                <svg class="w-16 h-16 text-gray-300 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                </svg>
                <p class="text-xl text-gray-600">אין היסטוריית חיפושים עדיין</p>
            </div>
        </div>

        <div class="mt-8 bg-gradient-to-r from-purple-600 to-blue-600 rounded-2xl shadow-xl p-6 text-white">
            <h3 class="text-xl font-bold mb-3">🚀 כיצד לשדרג לסקרייפינג אמיתי?</h3>
            <p class="mb-4">כרגע הבוט מציג תוצאות לדוגמה. כדי לקבל מחירים אמיתיים בזמן אמת, תוכל להתחבר ל:</p>
            <ul class="space-y-2">
                <li>• <strong>ScraperAPI</strong> - 1000 בקשות חינם לחודש</li>
                <li>• <strong>Bright Data</strong> - יש תוכנית חינמית</li>
                <li>• <strong>Apify</strong> - scrapers מוכנים להשכרת רכבים</li>
            </ul>
        </div>
    </div>

    <script>
        var companies = [
            { name: 'Shlomo Sixt', url: 'https://www.shlomo.co.il', color: 'bg-orange-500' },
            { name: 'Eldan', url: 'https://www.eldan.co.il', color: 'bg-blue-500' },
            { name: 'Budget', url: 'https://www.budget.co.il', color: 'bg-red-500' },
            { name: 'Hertz', url: 'https://www.hertz.co.il', color: 'bg-yellow-500' },
            { name: 'Cal Auto', url: 'https://www.calauto.co.il', color: 'bg-green-500' },
            { name: 'Avis', url: 'https://www.avis.co.il', color: 'bg-purple-500' },
            { name: 'Enterprise', url: 'https://www.enterprise.co.il', color: 'bg-teal-500' },
            { name: 'Dollar', url: 'https://www.dollar.co.il', color: 'bg-indigo-500' }
        ];

        var carTypes = ['קטן', 'בינוני', 'גדול', 'משפחתי', 'יוקרה'];
        var searchHistory = [];
        var currentResults = [];

        function switchTab(tab) {
            document.getElementById('search-section').classList.add('hidden');
            document.getElementById('results-section').classList.add('hidden');
            document.getElementById('history-section').classList.add('hidden');

            document.getElementById('tab-search').className = 'flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-white text-gray-600 hover:bg-gray-50';
            document.getElementById('tab-results').className = 'flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-white text-gray-600 hover:bg-gray-50';
            document.getElementById('tab-history').className = 'flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-white text-gray-600 hover:bg-gray-50';

            if (tab === 'search') {
                document.getElementById('search-section').classList.remove('hidden');
                document.getElementById('tab-search').className = 'flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-blue-600 text-white shadow-lg';
            } else if (tab === 'results') {
                document.getElementById('results-section').classList.remove('hidden');
                document.getElementById('tab-results').className = 'flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-blue-600 text-white shadow-lg';
                if (currentResults.length === 0) {
                    document.getElementById('no-results').classList.remove('hidden');
                }
            } else if (tab === 'history') {
                document.getElementById('history-section').classList.remove('hidden');
                document.getElementById('tab-history').className = 'flex items-center gap-2 px-6 py-3 rounded-lg font-semibold transition-all bg-blue-600 text-white shadow-lg';
            }
        }

        function generateMockResults(pickupDate, returnDate, promoCode) {
            var basePrice = 150 + Math.random() * 200;
            var start = new Date(pickupDate);
            var end = new Date(returnDate);
            var days = Math.ceil((end - start) / (1000 * 60 * 60 * 24));

            return companies.map(function(company, idx) {
                var priceVariation = (Math.random() - 0.5) * 100;
                var dailyRate = basePrice + priceVariation + (idx * 15);
                var totalPrice = dailyRate * days;
                var discount = promoCode ? Math.floor(totalPrice * (0.05 + Math.random() * 0.15)) : 0;
                var finalPrice = totalPrice - discount;

                return {
                    company: company.name,
                    carType: carTypes[Math.floor(Math.random() * carTypes.length)],
                    dailyRate: Math.round(dailyRate),
                    totalPrice: Math.round(totalPrice),
                    discount: Math.round(discount),
                    finalPrice: Math.round(finalPrice),
                    url: company.url,
                    color: company.color,
                    features: ['ביטוח מלא', 'ק״מ ללא הגבלה', 'נהג נוסף חינם'].slice(0, Math.floor(Math.random() * 3) + 1)
                };
            }).sort(function(a, b) { return a.finalPrice - b.finalPrice; });
        }

        function handleSearch() {
            var pickupDate = document.getElementById('pickup-date').value;
            var returnDate = document.getElementById('return-date').value;
            var location = document.getElementById('location').value;
            var promoCode = document.getElementById('promo-code').value;

            if (!pickupDate || !returnDate || !location) {
                alert('נא למלא את כל השדות');
                return;
            }

            switchTab('results');

            document.getElementById('loading-spinner').classList.remove('hidden');
            document.getElementById('results-list').innerHTML = '';
            document.getElementById('no-results').classList.add('hidden');

            setTimeout(function() {
                currentResults = generateMockResults(pickupDate, returnDate, promoCode);
                displayResults(currentResults);
                document.getElementById('loading-spinner').classList.add('hidden');
                document.getElementById('results-count').textContent = currentResults.length;

                var newSearch = {
                    id: Date.now(),
                    date: new Date().toLocaleString('he-IL'),
                    pickupDate: pickupDate,
                    returnDate: returnDate,
                    location: location,
                    promoCode: promoCode,
                    cheapest: currentResults[0]
                };
                searchHistory.unshift(newSearch);
                searchHistory = searchHistory.slice(0, 10);
                document.getElementById('history-count').textContent = searchHistory.length;
                updateHistoryDisplay();
            }, 2000);
        }

        function displayResults(results) {
            var resultsList = document.getElementById('results-list');
            resultsList.innerHTML = '';

            var maxPrice = Math.max.apply(Math, results.map(function(r) { return r.finalPrice; }));

            results.forEach(function(result, idx) {
                var isTop = idx === 0;
                var savings = maxPrice - result.finalPrice;

                var featuresHTML = result.features.map(function(f) { 
                    return '<span class="text-xs bg-blue-100 text-blue-700 px-2 py-1 rounded-full">' + f + '</span>'; 
                }).join('');

                var discountHTML = result.discount > 0 ? 
                    '<div class="mb-2"><span class="text-gray-400 line-through text-sm">₪' + result.totalPrice + '</span>' +
                    '<span class="mr-2 text-green-600 font-semibold text-sm">חסכת ₪' + result.discount + '</span></div>' : '';

                var topBadgeHTML = isTop ? 
                    '<div class="mt-4 bg-green-50 border border-green-200 rounded-lg p-3 flex items-center gap-2">' +
                    '<svg class="w-5 h-5 text-green-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">' +
                    '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 7h8m0 0v8m0-8l-8 8-4-4-6 6"></path></svg>' +
                    '<span class="text-green-800 font-semibold">🎉 המחיר הכי טוב! חסוך עד ₪' + savings + '</span></div>' : '';

                var resultHTML = 
                    '<div class="bg-white rounded-xl shadow-lg hover:shadow-2xl transition-all p-6 border-2 ' + (isTop ? 'border-green-400 ring-4 ring-green-100' : 'border-gray-100') + '">' +
                    '<div class="flex items-center justify-between flex-wrap gap-4">' +
                    '<div class="flex items-center gap-4">' +
                    '<div class="' + result.color + ' w-16 h-16 rounded-xl flex items-center justify-center text-white font-bold text-2xl shadow-lg">' +
                    result.company.charAt(0) + '</div>' +
                    '<div><h3 class="text-xl font-bold text-gray-800 mb-1">' + result.company + '</h3>' +
                    '<p class="text-gray-600">' + result.carType + ' • ₪' + result.dailyRate + ' ליום</p>' +
                    '<div class="flex gap-2 mt-2">' + featuresHTML + '</div></div></div>' +
                    '<div class="text-center">' + discountHTML +
                    '<div class="text-3xl font-bold text-gray-800">₪' + result.finalPrice + '</div>' +
                    '<div class="text-sm text-gray-500">מחיר כולל</div></div>' +
                    '<a href="' + result.url + '" target="_blank" rel="noopener noreferrer" ' +
                    'class="bg-blue-600 hover:bg-blue-700 text-white px-6 py-3 rounded-lg font-semibold transition-all flex items-center gap-2 shadow-lg hover:shadow-xl">' +
                    'להזמנה<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">' +
                    '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path></svg></a>' +
                    '</div>' + topBadgeHTML + '</div>';
                
                resultsList.innerHTML += resultHTML;
            });
        }

        function updateHistoryDisplay() {
            var historyList = document.getElementById('history-list');
            var noHistory = document.getElementById('no-history');

            if (searchHistory.length === 0) {
                noHistory.classList.remove('hidden');
                historyList.innerHTML = '';
                return;
            }

            noHistory.classList.add('hidden');
            historyList.innerHTML = searchHistory.map(function(item) {
                return '<div class="bg-white rounded-xl shadow-lg p-6">' +
                    '<div class="flex items-center justify-between">' +
                    '<div class="flex-1">' +
                    '<div class="flex items-center gap-3 mb-3">' +
                    '<svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">' +
                    '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>' +
                    '<span class="text-sm text-gray-500">' + item.date + '</span></div>' +
                    '<div class="grid md:grid-cols-3 gap-4 text-sm">' +
                    '<div><span class="text-gray-500">תאריכים:</span>' +
                    '<span class="font-semibold mr-2">' + item.pickupDate + ' - ' + item.returnDate + '</span></div>' +
                    '<div><span class="text-gray-500">מיקום:</span>' +
                    '<span class="font-semibold mr-2">' + item.location + '</span></div>' +
                    '<div><span class="text-gray-500">המחיר הזול ביותר:</span>' +
                    '<span class="font-semibold mr-2 text-green-600">' + item.cheapest.company + ' - ₪' + item.cheapest.finalPrice + '</span></div>' +
                    '</div></div>' +
                    '<div class="flex gap-2">' +
                    '<button onclick="loadFromHistory(' + item.id + ')" class="bg-blue-100 hover:bg-blue-200 text-blue-700 px-4 py-2 rounded-lg transition-colors">טען שוב</button>' +
                    '<button onclick="deleteHistory(' + item.id + ')" class="bg-red-100 hover:bg-red-200 text-red-700 p-2 rounded-lg transition-colors">' +
                    '<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">' +
                    '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path></svg>' +
                    '</button></div></div></div>';
            }).join('');
        }

        function loadFromHistory(id) {
            var item = searchHistory.find(function(h) { return h.id === id; });
            if (item) {
                document.getElementById('pickup-date').value = item.pickupDate;
                document.getElementById('return-date').value = item.returnDate;
                document.getElementById('location').value = item.location;
                document.getElementById('promo-code').value = item.promoCode || '';
                switchTab('search');
            }
        }

        function deleteHistory(id) {
            searchHistory = searchHistory.filter(function(h) { return h.id !== id; });
            document.getElementById('history-count').textContent = searchHistory.length;
            updateHistoryDisplay();
        }
    </script>
</body>
</html>
