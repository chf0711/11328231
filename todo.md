def add_task():
    print("Add task")

def show_tasks():
    print("Show tasks")

def main():
    while True:
        print("\n=== To-Do List 管理系統 ===")
        print("1. 顯示任務清單")
        print("2. 新增任務")
        print("3. 離開系統")
        
        choice = input("請選擇功能（輸入數字）：").strip()
        
        if choice == "1":
            show_tasks()
        elif choice == "2":
            add_task()
        elif choice == "3":
            print("感謝使用，再見！")
            break
        else:
            print("無效的選擇，請重新輸入。\n")
def complete_task():
    if not pending_tasks:
        print("\n目前沒有未完成的任務！\n")
        return

    show_tasks()
    try:
        task_idx = int(input("請輸入要完成的任務編號：")) - 1
        if 0 <= task_idx < len(pending_tasks):
            task = pending_tasks.pop(task_idx)
            completed_tasks.append(task)
            print(f"\n成功完成任務：{task['title']}\n")
        else:
            print("\n無效的編號！請重新選擇。\n")
    except ValueError:
        print("\n輸入無效！請輸入數字。\n")
        def delete_task():
    print("\n=== 刪除任務 ===")
    show_tasks()

    task_type = input("請選擇任務類型（1: 未完成, 2: 已完成）：").strip()
    if task_type not in ["1", "2"]:
        print("\n無效的選擇！請輸入 1 或 2。\n")
        return

    task_list = pending_tasks if task_type == "1" else completed_tasks
    if not task_list:
        print("\n選擇的任務清單中沒有任務。\n")
        return

    try:
        task_idx = int(input("請輸入要刪除的任務編號：")) - 1
        if 0 <= task_idx < len(task_list):
            task = task_list.pop(task_idx)
            print(f"\n成功刪除任務：{task['title']}\n")
        else:
            print("\n無效的編號！請重新選擇。\n")
    except ValueError:
        print("\n輸入無效！請輸入數字。\n")
        def main():
    while True:
        print("\n=== To-Do List 管理系統 ===")
        print("1. 顯示任務清單")
        print("2. 新增任務")
        print("3. 完成任務")
        print("4. 刪除任務")
        print("5. 離開系統")
        
        choice = input("請選擇功能（輸入數字）：").strip()
        
        if choice == "1":
            show_tasks()
        elif choice == "2":
            add_task()
        elif choice == "3":
            complete_task()
        elif choice == "4":
            delete_task()
        elif choice == "5":
            print("感謝使用，再見！")
            break
        else:
            print("無效的選擇，請重新輸入。\n")

# 啟動主程式
main()
# 啟動主程式
main()
# 全域變數：用來存儲任務
pending_tasks = []   # 待完成的任務清單
completed_tasks = [] # 已完成的任務清單
# 新增任務
def add_task():
    title = input("請輸入任務名稱：").strip()
    if not title:
        print("任務名稱不可為空！")
        return
    
    description = input("請輸入任務描述（可選）：").strip()
    due_date = input("請輸入完成期限（格式: YYYY-MM-DD，可選）：").strip()

    # 建立新任務
    new_task = {
        "title": title,
        "description": description or None, # 這邊用 None 的話，後面 task['description'][:40] 會產生錯誤！
        "due_date": due_date or None,
    }
    pending_tasks.append(new_task)
    print(f"\n成功新增任務：{new_task['title']}\n")
    # 顯示任務清單
def show_tasks():
    print("\n=== 任務清單 ===")
    print("未完成的任務：")
    if not pending_tasks:
        print("\n  目前沒有任何任務！\n")
    else:
        for idx, task in enumerate(pending_tasks, start=1):
            print(f"  {idx}. {task['title']} ({task['description'][:40]})") # 描述部份最多顯示 40 個字元
    
    print("\n已完成的任務：")
    if not completed_tasks:
        print("\n  目前沒有任何任務！\n")
    else:
        for idx, task in enumerate(completed_tasks, start=1):
            print(f"  {idx}. {task['title']} ({task['description'][:40]})") # 描述部份最多顯示 40 個字元
    print()
    === To-Do List 管理系統 ===
1. 顯示任務清單
2. 新增任務
3. 離開系統
請選擇功能（輸入數字）：2
請輸入任務名稱：Title 1
請輸入任務描述（可選）：Do the task
請輸入完成期限（格式: YYYY-MM-DD，可選）：2024-11-27

成功新增任務：Title 1


=== To-Do List 管理系統 ===
1. 顯示任務清單
2. 新增任務
3. 離開系統
請選擇功能（輸入數字）：1

=== 任務清單 ===
未完成的任務：
  1. Title 1 (Do the task)

已完成的任務：

  目前沒有任何任務！
background-color: green;  /* 設定綠色背景 */
color: white;            /* 設定白色文字 */
font-weight: bold;       /* 文字加粗 */
border-radius: 5px;      /* 圓角邊框 */
padding: 5px;            /* 內邊距 5px */

from PyQt6.QtWidgets import QApplication, QWidget, QMessageBox
from PyQt6 import uic
import sys

class ToDoApp(QWidget):
    def __init__(self):
        super().__init__()
        # 載入 UI
        uic.loadUi('todo_app.ui', self)

        # 連接功能
        self.addButton.clicked.connect(self.add_task)
        self.deleteButton.clicked.connect(self.delete_task)
        self.markCompleteButton.clicked.connect(self.mark_complete)

    def add_task(self):
        task = self.taskInput.text()
        if task.strip():
            self.taskList.addItem(task)
            self.taskInput.clear()
        else:
            QMessageBox.warning(self, "Error", "Task cannot be empty")

    def delete_task(self):
        selected_task = self.taskList.currentItem()
        if selected_task:
            self.taskList.takeItem(self.taskList.row(selected_task))
        else:
            QMessageBox.warning(self, "Error", "No task selected")

    def mark_complete(self):
        selected_task = self.taskList.currentItem()
        if selected_task:
            selected_task.setText(f"{selected_task.text()} (Completed)")
        else:
            QMessageBox.warning(self, "Error", "No task selected")

# 主程式
if __name__ == '__main__':
    app = QApplication(sys.argv)
    window = ToDoApp()
    window.show()
    sys.exit(app.exec())

    
