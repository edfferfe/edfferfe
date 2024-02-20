import tkinter as tk
import random
import time

class LotteryApp:
    def __init__(self, root):
        self.root = root
        self.root.title("彩票开奖")
        self.draw_count = 1
        
        self.label = tk.Label(root, text="欢迎来到彩票开奖！", font=("Helvetica", 16))
        self.label.pack(pady=10)
        
        self.draw_button = tk.Button(root, text="开始下一轮开奖", command=self.draw_lottery)
        self.draw_button.pack(pady=5)
        
        self.result_label = tk.Label(root, text="", font=("Helvetica", 14))
        self.result_label.pack(pady=10)
        
    def roll_dice(self):
        return sum(random.randint(1, 6) for _ in range(3))
    
    def draw_lottery(self):
        dice_sum = self.roll_dice()
        result = "小" if 3 <= dice_sum <= 10 else "大"
        
        self.result_label.config(text=f"第{self.draw_count}期开奖号码为：{dice_sum}\n开出的是：{result}！")
        self.draw_count += 1
        
        self.root.after(60000, self.update_draw_count)
        
    def update_draw_count(self):
        self.draw_button.config(state=tk.NORMAL)
        self.result_label.config(text="")
        
    def run(self):
        self.root.mainloop()

if __name__ == "__main__":
    root = tk.Tk()
    app = LotteryApp(root)
    app.run()
