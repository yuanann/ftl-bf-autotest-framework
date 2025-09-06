通用規則
我要使用  Stagehand 來建立自動化測試 
使用python 進行開發 
幫我開立python .env 
使用中文回應 

程式規範 
網址: https://sit-admin.fintech-life.com/ 
每個 功能和子功能 都用單一 function 來執行 
範例程式  

import asyncio
from playwright.async_api import async_playwright

# -------------------------------
# 登入功能
# -------------------------------
async def login(page, account, password):
    """自動登入系統"""
    await page.goto("https://sit-admin.fintech-life.com/#/login")

    # 輸入帳號密碼
    await page.fill('input[placeholder="帳號"]', account)
    await page.fill('input[placeholder="密碼"]', password)

    # 點擊登入按鈕
    login_button = page.get_by_role("button", name="登 入")
    await login_button.click()
    await capture_page_screenshot(page, name_prefix="login", wait_time=1)


# -------------------------------
# 系統角色功能測試
# -------------------------------
async def test_system_role(page):
    """測試系統角色功能"""
    print("進入 test_system_role")

    # 點擊左側選單「系統設定」
    system_settings = page.locator('span:has-text("系統設定")')
    await system_settings.click()

    # 點擊子選單「系統角色」
    system_role = page.locator('a:has-text("系統角色")')
    await system_role.click()

    # 等待頁面元素載入
    await page.wait_for_selector('text=系統角色')  # 替換成頁面上實際文字

# -------------------------------
# 截圖功能
# -------------------------------
async def capture_page_screenshot(page, name_prefix="screenshot", wait_time=2):
    """通用截圖函數"""
    import datetime
    import os
    import asyncio

    await asyncio.sleep(wait_time)
    timestamp = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
    path = f"{name_prefix}_{timestamp}.png"
    await page.screenshot(path=path, full_page=True)
    if os.path.exists(path):
        print(f"✅ 截圖已保存: {path}")
    return path


# -------------------------------
# 主程式
# -------------------------------
async def main():
    async with async_playwright() as p:
        browser = await p.chromium.launch(headless=False, slow_mo=200)
        page = await browser.new_page()

        # 登入
        await login(page, "zane.chen@fintech-life.com", "aA1234567890")

        # 系統角色功能測試
        await test_system_role(page)

        # 截圖（可選）
        await capture_page_screenshot(page, name_prefix="system_role_page", wait_time=2)

        # 保持觀察
        await asyncio.sleep(5)
        await browser.close()

# 執行
asyncio.run(main())  





