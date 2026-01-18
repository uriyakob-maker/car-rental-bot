[3חדשcar-rental-bot.HTML](https://github.com/user-attachments/files/24697245/3.car-rental-bot.HTML)
<!DOCTYPE html>
<html lang="he" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>בוט חכם לחיפוש טיסות</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { 
            font-family: Arial, sans-serif; 
        }
        .smart-badge { 
            animation: pulse 2s infinite; 
        }
        @keyframes pulse { 
            0%, 100% { opacity: 1; } 
            50% { opacity: 0.7; } 
        }
    </style>
</head>
<body class="bg-gradient-to-br from-purple-50 to-indigo-100 min-h-screen p-6">
    <div class="max-w-5xl mx-auto">
        <div class="bg-white rounded-2xl shadow-xl p-8 mb-6">
            <div class="flex items-center gap-3 mb-2">
                <svg class="w-10 h-10 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"></path>
                </svg>
                <div>
                    <h1 class="text-3xl font-bold text-gray-800">בוט חכם לחיפוש טיסות</h1>
                    <span class="smart-badge inline-block bg-purple-100 text-purple-800 text-xs font-semibold px-3 py-1 rounded-full mt-1">
                        מוצא טריקים לחסוך כסף
                    </span>
                </div>
            </div>

            <div class="bg-gradient-to-r from-purple-50 to-pink-50 border border-purple-200 rounded-lg p-4 mb-6 text-sm">
                <strong>הבוט החכם יעשה עבורך:</strong>
                <ul class="mr-4 mt-2 space-y-1">
                    <li>משווה כיוון אחד VS הלוך-חזור (למצוא חזור פיקטיבי זול!)</li>
                    <li>בודק תאריכים גמישים (7 ימים לפני ואחרי) למצוא את המחיר הזול ביותר</li>
                    <li>בודק כל אפשרויות העצירות</li>
                    <li>ממיין הכל מהזול ליקר עם המלצות</li>
                </ul>
            </div>

            <div class="space-y-4 mb-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">API Key</label>
                        <input type="text" id="apiKey" placeholder="הזן API Key מ-Amadeus" 
                            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">API Secret</label>
                        <input type="password" id="apiSecret" placeholder="הזן API Secret"
                            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2" id="origin-label">מוצא (קוד IATA)</label>
                        <input type="text" id="origin" placeholder="TLV" maxlength="3"
                            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent uppercase">
                        <p class="text-xs text-gray-500 mt-1">לדוגמה: TLV, JFK, LHR, DXB</p>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2" id="destination-label">יעד (קוד IATA)</label>
                        <input type="text" id="destination" placeholder="JFK" maxlength="3"
                            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent uppercase">
                        <p class="text-xs text-gray-500 mt-1">לדוגמה: LAX, CDG, SYD, NRT</p>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">תאריך מועדף (אופציונלי)</label>
                        <input type="date" id="preferredDate"
                            class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">מטבע</label>
                        <select id="currency" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                            <option value="USD">דולר אמריקאי ($)</option>
                            <option value="EUR">יורו (€)</option>
                            <option value="GBP">לירה שטרלינג (£)</option>
                            <option value="ILS">שקל (₪)</option>
                            <option value="AUD">דולר אוסטרלי (A$)</option>
                            <option value="CAD">דולר קנדי (C$)</option>
                            <option value="JPY">ין יפני (¥)</option>
                            <option value="AED">דירהם (د.إ)</option>
                            <option value="CNY">יואן סיני (¥)</option>
                            <option value="INR">רופי הודי (₹)</option>
                        </select>
                    </div>
                </div>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">מחלקת טיסה</label>
                        <select id="travelClass" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                            <option value="ECONOMY">אקונומי</option>
                            <option value="PREMIUM_ECONOMY">אקונומי פרמיום</option>
                            <option value="BUSINESS">עסקים</option>
                            <option value="FIRST">ראשונה</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">תשלום</label>
                        <select id="paymentType" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                            <option value="cash">מזומן/כרטיס</option>
                            <option value="points">נקודות (Miles/Points)</option>
                        </select>
                    </div>
                </div>

                <div class="flex gap-4 flex-wrap">
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="checkbox" id="exactDate" class="w-4 h-4 text-purple-600 rounded">
                        <span class="text-sm text-gray-700">דווקא התאריך שבחרתי</span>
                    </label>
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="checkbox" id="flexibleDates" checked class="w-4 h-4 text-purple-600 rounded">
                        <span class="text-sm text-gray-700">חיפוש תאריכים גמישים (7 ימים)</span>
                    </label>
                    <label class="flex items-center gap-2 cursor-pointer">
                        <input type="checkbox" id="checkRoundTrip" checked class="w-4 h-4 text-purple-600 rounded">
                        <span class="text-sm text-gray-700">בדוק גם הלוך-חזור (חזור פיקטיבי)</span>
                    </label>
                </div>
            </div>

            <button onclick="smartSearch()" id="searchBtn"
                class="w-full bg-gradient-to-r from-purple-600 to-pink-600 hover:from-purple-700 hover:to-pink-700 text-white font-semibold py-3 px-6 rounded-lg transition-all shadow-lg">
                🔍 חיפוש חכם - מצא את העסקה הכי טובה!
            </button>

            <div id="error" class="hidden mt-4 p-4 bg-red-50 border border-red-200 rounded-lg text-red-700"></div>
            <div id="loading" class="hidden mt-4">
                <div class="bg-purple-50 border border-purple-200 rounded-lg p-6 text-center">
                    <div class="inline-block animate-spin rounded-full h-12 w-12 border-b-2 border-purple-600 mb-3"></div>
                    <p class="text-purple-800 font-medium" id="loadingText">מחפש טיסות...</p>
                    <p class="text-purple-600 text-sm mt-2" id="progressText"></p>
                </div>
            </div>
        </div>

        <div id="results" class="hidden"></div>

        <div class="bg-blue-50 border border-blue-200 rounded-lg p-4 text-sm text-blue-800">
            <strong>הוראות התחלה מהירה:</strong>
            <p class="mt-2">הירשם ב-<a href="https://developers.amadeus.com/register" target="_blank" class="underline font-semibold">Amadeus (חינם)</a>, צור Self-Service App, והעתק את ה-API Key ו-Secret למעלה.</p>
        </div>
    </div>

    <script>
        const airportNames = {
            'TLV': 'תל אביב',
            'JFK': 'ניו יורק JFK',
            'EWR': 'ניו יורק ניוארק',
            'LGA': 'ניו יורק לה גווארדיה',
            'BUD': 'בודפשט',
            'LHR': 'לונדון היתרו',
            'LGW': 'לונדון גטוויק',
            'CDG': 'פריז שארל דה גול',
            'ORY': 'פריז אורלי',
            'FCO': 'רומא פיומיצ\'ינו',
            'BCN': 'ברצלונה',
            'MAD': 'מדריד',
            'AMS': 'אמסטרדם',
            'FRA': 'פרנקפורט',
            'MUC': 'מינכן',
            'VIE': 'וינה',
            'ZRH': 'ציריך',
            'ATH': 'אתונה',
            'IST': 'איסטנבול',
            'DXB': 'דובאי',
            'DOH': 'דוחא',
            'AUH': 'אבו דאבי',
            'CAI': 'קהיר',
            'JNB': 'יוהנסבורג',
            'LAX': 'לוס אנג\'לס',
            'SFO': 'סן פרנסיסקו',
            'ORD': 'שיקגו',
            'MIA': 'מיאמי',
            'BOS': 'בוסטון',
            'SEA': 'סיאטל',
            'DEN': 'דנוור',
            'ATL': 'אטלנטה',
            'DFW': 'דאלאס',
            'IAH': 'יוסטון',
            'YYZ': 'טורונטו',
            'YVR': 'ונקובר',
            'MEX': 'מקסיקו סיטי',
            'GRU': 'סאו פאולו',
            'EZE': 'בואנוס איירס',
            'LIM': 'לימה',
            'BOG': 'בוגוטה',
            'SCL': 'סנטיאגו',
            'SYD': 'סידני',
            'MEL': 'מלבורן',
            'AKL': 'אוקלנד',
            'NRT': 'טוקיו נריטה',
            'HND': 'טוקיו האנדה',
            'ICN': 'סיאול',
            'PEK': 'בייג\'ינג',
            'PVG': 'שנחאי',
            'HKG': 'הונג קונג',
            'SIN': 'סינגפור',
            'BKK': 'בנגקוק',
            'KUL': 'קואלה לומפור',
            'DEL': 'ניו דלהי',
            'BOM': 'מומבאי',
            'JED': 'ג\'דה',
            'RUH': 'ריאד',
            'AMM': 'עמאן',
            'BEY': 'ביירות',
            'PRG': 'פראג',
            'WAW': 'ורשה',
            'BRU': 'בריסל',
            'CPH': 'קופנהגן',
            'ARN': 'סטוקהולם',
            'OSL': 'אוסלו',
            'HEL': 'הלסינקי',
            'DUB': 'דבלין',
            'LIS': 'ליסבון',
            'OTP': 'בוקרשט'
        };

        let accessToken = '';

        // Add event listeners when page loads
        document.addEventListener('DOMContentLoaded', function() {
            document.getElementById('origin').addEventListener('input', function() {
                displayAirportName('origin');
            });
            document.getElementById('destination').addEventListener('input', function() {
                displayAirportName('destination');
            });
        });

        function displayAirportName(field) {
            const input = document.getElementById(field);
            const label = document.getElementById(field + '-label');
            const value = input.value.toUpperCase().trim();
            
            if (value.length === 3 && airportNames[value]) {
                label.innerHTML = (field === 'origin' ? 'מוצא' : 'יעד') + ' <span class="text-green-600">✓ ' + airportNames[value] + '</span>';
            } else {
                label.textContent = field === 'origin' ? 'מוצא (קוד IATA)' : 'יעד (קוד IATA)';
            }
        }

        async function getAccessToken() {
            const apiKey = document.getElementById('apiKey').value;
            const apiSecret = document.getElementById('apiSecret').value;

            const response = await fetch('https://test.api.amadeus.com/v1/security/oauth2/token', {
                method: 'POST',
                headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
                body: 'grant_type=client_credentials&client_id=' + apiKey + '&client_secret=' + apiSecret
            });
            
            const data = await response.json();
            if (data.access_token) {
                accessToken = data.access_token;
                return data.access_token;
            }
            throw new Error('שגיאה באימות API');
        }

        function updateProgress(text) {
            document.getElementById('progressText').textContent = text;
        }

        function formatDate(date) {
            const year = date.getFullYear();
            const month = String(date.getMonth() + 1).padStart(2, '0');
            const day = String(date.getDate()).padStart(2, '0');
            return year + '-' + month + '-' + day;
        }

        async function searchFlightsForDate(origin, destination, date, token, isRoundTrip, travelClass, currency) {
            let url = 'https://test.api.amadeus.com/v2/shopping/flight-offers?originLocationCode=' + origin + '&destinationLocationCode=' + destination + '&departureDate=' + date + '&adults=1&nonStop=false&currencyCode=' + currency + '&travelClass=' + travelClass + '&max=5';
            
            if (isRoundTrip) {
                const returnDate = new Date(date);
                returnDate.setDate(returnDate.getDate() + 7);
                url += '&returnDate=' + formatDate(returnDate);
            }

            const response = await fetch(url, {
                headers: { 'Authorization': 'Bearer ' + token }
            });

            const data = await response.json();
            const flights = data.data || [];
            
            flights.forEach(flight => {
                if (flight.travelerPricings && flight.travelerPricings[0]) {
                    const fareOptions = flight.travelerPricings[0].fareOption || '';
                    const validatingAirline = flight.validatingAirlineCodes ? flight.validatingAirlineCodes[0] : null;
                    
                    flight.availableForMiles = fareOptions.includes('AWARD') || fareOptions.includes('MILES');
                    flight.validatingAirline = validatingAirline;
                }
            });
            
            return flights;
        }

        async function smartSearch() {
            const apiKey = document.getElementById('apiKey').value;
            const apiSecret = document.getElementById('apiSecret').value;
            const origin = document.getElementById('origin').value.toUpperCase();
            const destination = document.getElementById('destination').value.toUpperCase();
            const preferredDate = document.getElementById('preferredDate').value;
            const flexibleDates = document.getElementById('flexibleDates').checked;
            const checkRoundTrip = document.getElementById('checkRoundTrip').checked;
            const travelClass = document.getElementById('travelClass').value;
            const paymentType = document.getElementById('paymentType').value;
            const currency = document.getElementById('currency').value;
            
            const errorDiv = document.getElementById('error');
            const loadingDiv = document.getElementById('loading');
            const resultsDiv = document.getElementById('results');
            
            errorDiv.classList.add('hidden');
            resultsDiv.classList.add('hidden');
            
            if (!apiKey || !apiSecret || !origin || !destination) {
                showError('אנא מלא את כל השדות הנדרשים');
                return;
            }

            loadingDiv.classList.remove('hidden');
            updateProgress('מתחבר ל-API...');

            try {
                const token = await getAccessToken();
                
                const baseDate = preferredDate ? new Date(preferredDate) : new Date();
                baseDate.setDate(baseDate.getDate() + 7);
                
                const exactDate = document.getElementById('exactDate').checked;
                const datesToCheck = [baseDate];
                
                if (flexibleDates && !exactDate) {
                    for (let i = 1; i <= 7; i++) {
                        const before = new Date(baseDate);
                        before.setDate(before.getDate() - i);
                        datesToCheck.push(before);
                        
                        const after = new Date(baseDate);
                        after.setDate(after.getDate() + i);
                        datesToCheck.push(after);
                    }
                }

                let allFlights = [];
                let searchCount = 0;
                const totalSearches = datesToCheck.length * (checkRoundTrip ? 2 : 1);

                for (const date of datesToCheck) {
                    const dateStr = formatDate(date);
                    
                    updateProgress('מחפש טיסות לתאריך ' + new Date(date).toLocaleDateString('he-IL') + ' (' + (++searchCount) + '/' + totalSearches + ')...');
                    
                    const oneWayFlights = await searchFlightsForDate(origin, destination, dateStr, token, false, travelClass, currency);
                    oneWayFlights.forEach(f => {
                        f.searchType = 'כיוון אחד';
                        f.searchDate = dateStr;
                        f.paymentType = paymentType;
                    });
                    allFlights.push(...oneWayFlights);
                    
                    if (checkRoundTrip) {
                        updateProgress('בודק הלוך-חזור לתאריך ' + new Date(date).toLocaleDateString('he-IL') + ' (' + (++searchCount) + '/' + totalSearches + ')...');
                        await new Promise(resolve => setTimeout(resolve, 500));
                        
                        const roundTripFlights = await searchFlightsForDate(origin, destination, dateStr, token, true, travelClass, currency);
                        roundTripFlights.forEach(f => {
                            f.searchType = 'הלוך-חזור (חזור פיקטיבי!)';
                            f.searchDate = dateStr;
                            f.isTrick = true;
                            f.paymentType = paymentType;
                        });
                        allFlights.push(...roundTripFlights);
                    }
                    
                    await new Promise(resolve => setTimeout(resolve, 300));
                }

                if (allFlights.length > 0) {
                    allFlights.sort((a, b) => parseFloat(a.price.total) - parseFloat(b.price.total));
                    displaySmartResults(allFlights.slice(0, 15), origin, destination);
                } else {
                    showError('לא נמצאו טיסות');
                }
            } catch (err) {
                showError(err.message || 'שגיאה בחיפוש');
            } finally {
                loadingDiv.classList.add('hidden');
            }
        }

        function showError(message) {
            const errorDiv = document.getElementById('error');
            errorDiv.textContent = message;
            errorDiv.classList.remove('hidden');
        }

        function getAirlineWebsite(airlineCode) {
            const airlines = {
                'LY': 'https://www.elal.com',
                'TK': 'https://www.turkishairlines.com',
                'LH': 'https://www.lufthansa.com',
                'BA': 'https://www.britishairways.com',
                'AF': 'https://www.airfrance.com',
                'KL': 'https://www.klm.com',
                'EK': 'https://www.emirates.com',
                'QR': 'https://www.qatarairways.com',
                'LX': 'https://www.swiss.com',
                'OS': 'https://www.austrian.com',
                'AZ': 'https://www.ita-airways.com',
                'AA': 'https://www.aa.com',
                'DL': 'https://www.delta.com',
                'UA': 'https://www.united.com',
                'AC': 'https://www.aircanada.com',
                'SU': 'https://www.aeroflot.ru',
                'EY': 'https://www.etihad.com',
                'SV': 'https://www.saudia.com',
                'MS': 'https://www.egyptair.com',
                'RJ': 'https://www.rj.com',
                'W6': 'https://wizzair.com',
                'FR': 'https://www.ryanair.com',
                'U2': 'https://www.easyjet.com',
                'VY': 'https://www.vueling.com',
                'TP': 'https://www.flytap.com',
                'SQ': 'https://www.singaporeair.com',
                'CX': 'https://www.cathaypacific.com',
                'NH': 'https://www.ana.co.jp',
                'JL': 'https://www.jal.com',
                'QF': 'https://www.qantas.com',
                'NZ': 'https://www.airnewzealand.com',
                'SA': 'https://www.flysaa.com',
                'ET': 'https://www.ethiopianairlines.com',
                'KE': 'https://www.koreanair.com',
                'OZ': 'https://flyasiana.com',
                'AI': 'https://www.airindia.com',
                'TG': 'https://www.thaiairways.com',
                'MH': 'https://www.malaysiaairlines.com',
                'BR': 'https://www.evaair.com',
                'AV': 'https://www.avianca.com',
                'LA': 'https://www.latam.com',
                'AM': 'https://www.aeromexico.com',
                'CM': 'https://www.copaair.com'
            };
            return airlines[airlineCode] || 'https://www.google.com/flights';
        }

        function getAirlineName(airlineCode) {
            const airlines = {
                'LY': 'אל על',
                'TK': 'טורקיש איירליינס',
                'LH': 'לופטהנזה',
                'BA': 'בריטיש איירווייז',
                'AF': 'אייר פראנס',
                'KL': 'KLM',
                'EK': 'אמיריטס',
                'QR': 'קטאר איירווייז',
                'LX': 'סוויס',
                'OS': 'אוסטריאן',
                'AZ': 'ITA איירווייז',
                'AA': 'אמריקן איירליינס',
                'DL': 'דלתא',
                'UA': 'יונייטד',
                'AC': 'אייר קנדה',
                'SU': 'אירופלוט',
                'EY': 'אתיחאד',
                'SV': 'סעודיה',
                'MS': 'מצרים אייר',
                'RJ': 'רויאל ג׳ורדניאן',
                'W6': 'Wizz Air',
                'FR': 'Ryanair',
                'U2': 'EasyJet',
                'VY': 'Vueling',
                'TP': 'TAP פורטוגל',
                'SQ': 'סינגפור איירליינס',
                'CX': 'קאתיי פסיפיק',
                'NH': 'ANA',
                'JL': 'ג\'פן איירליינס',
                'QF': 'קוואנטס',
                'NZ': 'אייר ניו זילנד',
                'SA': 'דרום אפריקה איירווייז',
                'ET': 'אתיופיאן איירליינס',
                'KE': 'קוריאן אייר',
                'OZ': 'אסיאנה איירליינס',
                'AI': 'אייר אינדיה',
                'TG': 'תאי איירווייז',
                'MH': 'מלזיה איירליינס',
                'BR': 'EVA Air',
                'AV': 'אוויאנקה',
                'LA': 'LATAM',
                'AM': 'אירומקסיקו',
                'CM': 'קופה איירליינס'
            };
            return airlines[airlineCode] || airlineCode;
        }

        function displaySmartResults(flights, origin, destination) {
            const resultsDiv = document.getElementById('results');
            
            const cheapest = flights[0];
            const savings = flights.length > 1 ? 
                ((parseFloat(flights[flights.length - 1].price.total) - parseFloat(cheapest.price
