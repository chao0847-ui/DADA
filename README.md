
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>美甲管理系統</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Microsoft YaHei', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow:  0 10px 40px rgba(0,0,0,0.2);
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }
        
        header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
        }
        
        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            padding: 30px;
        }
        
        .section {
            background: #f8f9fa;
            padding:  25px;
            border-radius:  8px;
            border-left: 4px solid #667eea;
        }
        
        .section h2 {
            color: #333;
            margin-bottom: 20px;
            font-size: 1.5em;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            color: #555;
            font-weight: bold;
        }
        
        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 14px;
            font-family: inherit;
        }
        
        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 5px rgba(102, 126, 234, 0.3);
        }
        
        button {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 12px 25px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
            font-weight:  bold;
            transition: transform 0.2s, box-shadow 0.2s;
        }
        
        button:hover {
            transform:  translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }
        
        button:active {
            transform: translateY(0);
        }
        
        .list-item {
            background: white;
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 5px;
            border-left: 3px solid #764ba2;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .list-item strong {
            color: #333;
        }
        
        .btn-small {
            padding: 6px 12px;
            font-size: 12px;
            margin-left: 10px;
            background: #dc3545;
        }
        
        .btn-small:hover {
            background:  #c82333;
        }
        
        .appointment-slot {
            background: white;
            padding: 15px;
            margin-bottom:  10px;
            border-radius: 5px;
            border-left: 3px solid #28a745;
            cursor: pointer;
            transition: background 0.2s;
        }
        
        . appointment-slot:hover {
            background: #f0f0f0;
        }
        
        .appointment-slot.booked {
            background: #fff3cd;
            border-left-color: #ffc107;
        }
        
        .appointment-slot.available {
            background: #d4edda;
            border-left-color: #28a745;
        }
        
        .time-slots {
            display: grid;
            grid-template-columns: 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .tab-buttons {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .tab-buttons button {
            flex: 1;
            min-width: 100px;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 15px;
            margin-bottom:  20px;
        }
        
        .stat-box {
            background: white;
            padding: 15px;
            border-radius: 5px;
            text-align: center;
            border-top: 3px solid #667eea;
        }
        
        .stat-box h3 {
            color:  #667eea;
            font-size: 2em;
            margin:  5px 0;
        }
        
        .stat-box p {
            color: #999;
            font-size: 12px;
        }
        
        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .stats {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>✨ 美甲沙龍管理系統 ✨</h1>
            <p>專業的客戶與預約管理平台</p>
        </header>
        
        <div class="main-content">
            <!-- 左側：客戶管理 -->
            <div class="section">
                <h2>👥 客戶管理</h2>
                
                <div class="stats">
                    <div class="stat-box">
                        <h3 id="totalCustomers">0</h3>
                        <p>總客戶數</p>
                    </div>
                    <div class="stat-box">
                        <h3 id="totalMembers">0</h3>
                        <p>會員數</p>
                    </div>
                    <div class="stat-box">
                        <h3 id="totalVisits">0</h3>
                        <p>造訪記錄</p>
                    </div>
                </div>
                
                <h3 style="margin-top: 20px; margin-bottom: 15px; color: #333;">新增客戶 / 會員</h3>
                
                <div class="form-group">
                    <label for="customerName">客戶名稱 *</label>
                    <input type="text" id="customerName" placeholder="輸入客戶名稱">
                </div>
                
                <div class="form-group">
                    <label for="customerPhone">電話 *</label>
                    <input type="tel" id="customerPhone" placeholder="輸入電話號碼">
                </div>
                
                <div class="form-group">
                    <label for="customerEmail">信箱</label>
                    <input type="email" id="customerEmail" placeholder="輸入信箱（選填）">
                </div>
                
                <div class="form-group">
                    <label for="isMember">
                        <input type="checkbox" id="isMember" style="width: auto; margin-right: 8px;">
                        是會員
                    </label>
                </div>
                
                <div class="form-group" id="memberFieldsGroup" style="display: none;">
                    <label for="membershipLevel">會員等級</label>
                    <select id="membershipLevel">
                        <option value="bronze">銅卡會員</option>
                        <option value="silver">銀卡會員</option>
                        <option value="gold">金卡會員</option>
                        <option value="platinum">白金會員</option>
                    </select>
                </div>
                
                <div class="form-group" id="memberFieldsGroup2" style="display: none;">
                    <label for="points">會員積分</label>
                    <input type="number" id="points" placeholder="0" min="0" value="0">
                </div>
                
                <button onclick="addCustomer()">➕ 新增客戶</button>
                
                <h3 style="margin-top: 25px; margin-bottom: 15px; color: #333;">客戶列表</h3>
                <div id="customerList" style="max-height: 400px; overflow-y: auto;"></div>
            </div>
            
            <!-- 右側：預約管理 -->
            <div class="section">
                <h2>📅 預約管理</h2>
                
                <h3 style="margin-bottom: 15px; color: #333;">新增預約</h3>
                
                <div class="form-group">
                    <label for="appointmentCustomer">選擇客戶 *</label>
                    <select id="appointmentCustomer">
                        <option value="">-- 請選擇客戶 --</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="appointmentDate">預約日期 *</label>
                    <input type="date" id="appointmentDate">
                </div>
                
                <div class="form-group">
                    <label>預約時段 *</label>
                    <div class="time-slots">
                        <label style="display: flex; align-items: center; margin-bottom: 0;">
                            <input type="radio" name="appointmentTime" value="morning" style="width: auto; margin-right: 10px;">
                            <strong>上午時段 (10:30 - 12:30)</strong>
                        </label>
                        <label style="display: flex; align-items:  center; margin-bottom: 0;">
                            <input type="radio" name="appointmentTime" value="afternoon" style="width:  auto; margin-right: 10px;">
                            <strong>下午時段 (14:00 - 17:00)</strong>
                        </label>
                        <label style="display: flex; align-items: center; margin-bottom:  0;">
                            <input type="radio" name="appointmentTime" value="evening" style="width: auto; margin-right:  10px;">
                            <strong>晚間時段 (18:00 - 20:00)</strong>
                        </label>
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="serviceType">服務項目</label>
                    <select id="serviceType">
                        <option value="">選擇服務項目</option>
                        <option value="nail">指甲彩繪</option>
                        <option value="gel">光療指甲</option>
                        <option value="extension">指甲延長</option>
                        <option value="removal">卸甲</option>
                        <option value="foot">腳部護理</option>
                        <option value="other">其他</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="appointmentNotes">備註</label>
                    <textarea id="appointmentNotes" placeholder="輸入任何特殊要求或備註" rows="3"></textarea>
                </div>
                
                <button onclick="addAppointment()">➕ 新增預約</button>
                
                <h3 style="margin-top: 25px; margin-bottom: 15px; color: #333;">預約日程</h3>
                
                <div class="form-group">
                    <label for="viewDate">查看日期</label>
                    <input type="date" id="viewDate">
                </div>
                
                <button onclick="viewAppointments()" style="width: 100%; margin-bottom: 15px;">🔍 查看預約</button>
                
                <div id="appointmentsList" style="max-height: 400px; overflow-y: auto;"></div>
            </div>
        </div>
    </div>

    <script>
        // 數據存儲
        let customers = JSON.parse(localStorage.getItem('customers')) || [];
        let appointments = JSON.parse(localStorage.getItem('appointments')) || [];
        let visits = JSON.parse(localStorage.getItem('visits')) || [];

        // 監聽會員複選框
        document.getElementById('isMember').addEventListener('change', function() {
            document.getElementById('memberFieldsGroup').style.display = this.checked ?  'block' : 'none';
            document.getElementById('memberFieldsGroup2').style.display = this.checked ? 'block' : 'none';
        });

        // 設置今天的日期作為預約日期的預設值
        document.getElementById('appointmentDate').valueAsDate = new Date();
        document.getElementById('viewDate').valueAsDate = new Date();

        // 新增客戶
        function addCustomer() {
            const name = document.getElementById('customerName').value.trim();
            const phone = document.getElementById('customerPhone').value.trim();
            const email = document.getElementById('customerEmail').value.trim();
            const isMember = document.getElementById('isMember').checked;
            const membershipLevel = document.getElementById('membershipLevel').value;
            const points = parseInt(document.getElementById('points').value) || 0;

            if (! name || !phone) {
                alert('❌ 請輸入客戶名稱和電話');
                return;
            }

            const customer = {
                id: Date.now(),
                name,
                phone,
                email,
                isMember,
                membershipLevel:  isMember ? membershipLevel : null,
                points:  isMember ? points : 0,
                createdAt: new Date().toLocaleDateString('zh-TW')
            };

            customers.push(customer);
            saveData();
            displayCustomers();
            updateAppointmentCustomerSelect();
            clearCustomerForm();
            alert('✅ 客戶已成功新增！');
        }

        // 清除客戶表單
        function clearCustomerForm() {
            document.getElementById('customerName').value = '';
            document.getElementById('customerPhone').value = '';
            document.getElementById('customerEmail').value = '';
            document.getElementById('isMember').checked = false;
            document.getElementById('membershipLevel').value = 'bronze';
            document.getElementById('points').value = '0';
            document.getElementById('memberFieldsGroup').style.display = 'none';
            document. getElementById('memberFieldsGroup2').style.display = 'none';
        }

        // 顯示客戶列表
        function displayCustomers() {
            const list = document.getElementById('customerList');
            list.innerHTML = '';

            if (customers.length === 0) {
                list.innerHTML = '<p style="text-align: center; color: #999;">還沒有客戶記錄</p>';
                return;
            }

            customers.forEach(customer => {
                const item = document.createElement('div');
                item.className = 'list-item';
                item.innerHTML = `
                    <div>
                        <strong>${customer. name}</strong> <br>
                        <small>📞 ${customer.phone}</small> ${customer.email ?  `<br><small>📧 ${customer.email}</small>` : ''} <br>
                        ${customer.isMember ? `<small style="color: #667eea;">⭐ ${customer.membershipLevel. toUpperCase()} | 積分:  ${customer.points}</small>` : '<small style="color: #999;">普通客戶</small>'} <br>
                        <small style="color: #ccc;">加入:  ${customer.createdAt}</small>
                    </div>
                    <button class="btn-small" onclick="deleteCustomer(${customer.id})">刪除</button>
                `;
                list.appendChild(item);
            });

            updateStats();
        }

        // 刪除客戶
        function deleteCustomer(id) {
            if (confirm('確定要刪除此客戶嗎？')) {
                customers = customers.filter(c => c.id !== id);
                saveData();
                displayCustomers();
                updateAppointmentCustomerSelect();
            }
        }

        // 新增預約
        function addAppointment() {
            const customerId = parseInt(document.getElementById('appointmentCustomer').value);
            const date = document.getElementById('appointmentDate').value;
            const time = document.querySelector('input[name="appointmentTime"]:checked')?.value;
            const serviceType = document.getElementById('serviceType').value;
            const notes = document.getElementById('appointmentNotes').value.trim();

            if (!customerId || !date || ! time) {
                alert('❌ 請填入客戶、日期和時段');
                return;
            }

            const customer = customers.find(c => c.id === customerId);
            if (!customer) {
                alert('❌ 客戶不存在');
                return;
            }

            // 檢查是否已預約相同時段
            const existingAppointment = appointments.find(a => 
                a.customerId === customerId && a.date === date && a.time === time
            );

            if (existingAppointment) {
                alert('❌ 該時段已被預約，請選擇其他時段');
                return;
            }

            const appointment = {
                id:  Date.now(),
                customerId,
                customerName: customer.name,
                date,
                time,
                serviceType,
                notes,
                status: 'confirmed',
                createdAt: new Date().toLocaleString('zh-TW')
            };

            appointments.push(appointment);
            saveData();
            clearAppointmentForm();
            alert('✅ 預約已成功新增！');
            viewAppointments();
        }

        // 清除預約表單
        function clearAppointmentForm() {
            document.getElementById('appointmentCustomer').value = '';
            document.getElementById('appointmentDate').valueAsDate = new Date();
            document.querySelectorAll('input[name="appointmentTime"]').forEach(r => r.checked = false);
            document.getElementById('serviceType').value = '';
            document.getElementById('appointmentNotes').value = '';
        }

        // 查看預約
        function viewAppointments() {
            const date = document.getElementById('viewDate').value;
            const list = document.getElementById('appointmentsList');
            list.innerHTML = '';

            const dayAppointments = appointments.filter(a => a.date === date);

            if (dayAppointments. length === 0) {
                list.innerHTML = '<p style="text-align: center; color:  #999;">此日期沒有預約</p>';
                return;
            }

            // 按時段排序
            const timeOrder = { morning: 1, afternoon: 2, evening:  3 };
            dayAppointments.sort((a, b) => timeOrder[a.time] - timeOrder[b.time]);

            const timeSlots = {
                morning: '上午 (10:30 - 12:30)',
                afternoon: '下午 (14:00 - 17:00)',
                evening: '晚間 (18:00 - 20:00)'
            };

            dayAppointments.forEach(appointment => {
                const item = document.createElement('div');
                item.className = 'appointment-slot booked';
                item.innerHTML = `
                    <strong>${appointment.customerName}</strong> - <span style="color: #667eea; font-weight: bold;">${timeSlots[appointment.time]}</span> <br>
                    ${appointment. serviceType ?  `<small>服務:  ${appointment.serviceType}</small> <br>` : ''}
                    ${appointment.notes ? `<small>備註: ${appointment.notes}</small> <br>` : ''}
                    <small style="color:  #999;">預約時間: ${appointment.createdAt}</small>
                    <button class="btn-small" onclick="deleteAppointment(${appointment.id})" style="margin-top: 8px;">取消</button>
                `;
                list.appendChild(item);
            });

            // 顯示空檔
            const booked = new Set(dayAppointments.map(a => a.time));
            const allSlots = ['morning', 'afternoon', 'evening'];
            
            allSlots.forEach(slot => {
                if (!booked.has(slot)) {
                    const item = document.createElement('div');
                    item.className = 'appointment-slot available';
                    item. innerHTML = `
                        <strong style="color: #28a745;">✅ ${timeSlots[slot]} - 可預約</strong>
                    `;
                    list.appendChild(item);
                }
            });
        }

        // 刪除預約
        function deleteAppointment(id) {
            if (confirm('確定要取消此預約嗎？')) {
                appointments = appointments.filter(a => a.id !== id);
                saveData();
                const date = document.getElementById('viewDate').value;
                document.getElementById('viewDate').valueAsDate = new Date(date);
                viewAppointments();
            }
        }

        // 更新客戶選擇列表
        function updateAppointmentCustomerSelect() {
            const select = document.getElementById('appointmentCustomer');
            select.innerHTML = '<option value="">-- 請選擇客戶 --</option>';
            
            customers.forEach(customer => {
                const option = document.createElement('option');
                option.value = customer.id;
                option.textContent = `${customer.name} (${customer.phone})`;
                select.appendChild(option);
            });
        }

        // 更新統計數據
        function updateStats() {
            document.getElementById('totalCustomers').textContent = customers.length;
            document.getElementById('totalMembers').textContent = customers.filter(c => c.isMember).length;
            document.getElementById('totalVisits').textContent = appointments.length;
        }

        // 保存數據到本地存儲
        function saveData() {
            localStorage.setItem('customers', JSON.stringify(customers));
            localStorage.setItem('appointments', JSON. stringify(appointments));
            localStorage. setItem('visits', JSON.stringify(visits));
        }

        // 初始化
        function init() {
            displayCustomers();
            updateAppointmentCustomerSelect();
            updateStats();
        }

        init();
    </script>
</body>
</html>
