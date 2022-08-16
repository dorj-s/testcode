# testcode
import math
import csv
import PySimpleGUI as sg
import tkinter as tk
import tkinter.messagebox

n=0
ts=[]
te=[]

# print(n)
# print(oxs[0])
# print(oxe[3])
	# sxs=oxe
	# oxs=float(row[0])
	# oxe=float(row[1])
	# print(oxs)
	# print(oxe)
	# if n >= 2 :
	# 	sxe=oxs
	# 	print(sxs)
	# 	print(sxe)



# キャンバスの横方向・縦方向のサイズ（px）
CANVAS_SIZE = 400

# 色の設定
BOARD_COLOR = "white" # 盤面の背景色
OPE_COLOR = 'black' # あなたの石の色
STO_COLOR = 'gray' # 相手の石の色

#稼働中・停止中識別を示す値
ope=1
sto=0

class Main():
	def __init__(self, master):
		#'''コンストラクタ'''
		self.color = { # 稼働中と停止中を識別する色の辞書
			ope : OPE_COLOR,
			sto : STO_COLOR
		}


		# ウィジェットの作成
		self.createWidgets()
		# オセロゲームの初期化
		self.initOthello()

	def createWidgets(self):
		self.canvas = tk.Canvas(
			bg=BOARD_COLOR,
			width=CANVAS_SIZE*1.5, # +1は枠線描画のため
			height=CANVAS_SIZE, # +1は枠線描画のため
			highlightthickness=0
		)
		self.canvas.pack(padx=10, pady=10)

	def setEvents(self): #イベントを設定する
		# キャンバス上のマウスクリックを受け付ける
		self.canvas.bind('<ButtonPress>', self.click)

	def initOthello(self): #初期化を行う

		n=0
		with  open("input.csv", "r") as f:
			reader=csv.reader(f)
			for row in reader:
				n=n+1
				ts.append(float(row[0]))
				te.append(float(row[1]))

		for i in range(n):
			ots=ts[i]*20
			ote=te[i]*20

			# print(i)
			# print("ope")
			# print(ots)
			# print(ote)

			# 圧延中の長方形を描画
			tag_name = 'ope_' + str(i)
			self.canvas.create_rectangle(
				ots, 20,
				ote, 370,
				fill=self.color[ope],
				tag=tag_name,
			)

			if i >= 1:
				sts=te[i-1]*20
				ste=ots
				# print("sto")
				# print(sts)
				# print(ste)

				# 停止中の長方形を描画
				tag_name = 'sto_' + str(i)
				self.canvas.create_rectangle(
					sts, 20,
					ste, 370,
					fill=self.color[sto],
					tag=tag_name,
				)
	def click(self, event): #クリックされた時の処理'

		# クリックされた位置がどのマスであるかを計算
		x = event.x // self.square_size
		y = event.y // self.square_size

		if self.checkPlacable(x, y):
			# 次に石を置けるマスであれば石を置く
			self.place(x, y, self.color[self.player])





# スクリプト処理ここから
app = tkinter.Tk()
app.title('test')
othello = Main(app)
app.mainloop()



# TODO: Check

# param = {}

# with open("komoku.csv", "r") as f:

# 	param["task"] = [i for i in csv.reader(f)]

# nc = 5
# rdi_list = [[name, f"-hd_rdi_{i:02d}-"] for i, name, in enumerate(param["task"])]
# hd_rdi = [sg.Radio(name, group_id="hd_rdi", key=key, p=0, enable_events=True) for name, key in rdi_list]
# rt = [sg.Column([[rd for rd in hd_rdi[i::nc]] for i in range(nc)])]

# #1. layout
# layout = [
# 	rt
# ]

# #2. create window
# window = sg.Window(
# 	title = "Window title",
# 	layout=layout
# )
# window.finalize()

# #3. GUI処理
# while True:
# 	event, values = window.read(timeout=None)
# 	if event is None:
# 		break
# window.close()


