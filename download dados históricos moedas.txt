pegar o banco de dados de todas as opções binárias de moedas
fazer o levantamento de mhi de todas com gale 1 apenas
fazer predição de mhi com learning machine

----------------------

MODE= 'PRACTICE'
Iq.change_balance(MODE)

#compra simples no binário
#duration = 1
#Iq.buy(1, asset, "put", duration)
ticks=[]

def get_historical(interval):
	end_from_time = time.time()
	for i in range (365):
		candles=[]
		candles=Iq.get_candles(asset, int(interval), 1440, end_from_time)
		cds=[]
		for candle in candles:
			cd_handle={}
			if candle["open"]:
				cd_handle['open'] = candle["open"]
				cd_candle['high'] = candle["max"]
				cd_candle['low'] = candle["min"]
				cd_handle['created_at'] = dt.datetime.fromtimesstamp(candle["from"]).isoformat()
				cd_handle['timestamp'] = candle["from"]
				cd_handle['volume'] = candle["volume"]
				cds.append(cd_handle)
		global ticks
		ticks = cds + ticks
		end_from_time = int(cds[0]["timestamp"]) -1
		
def get_tickers(interval):
	maxdict = 5
	Iq.start_candles_stream(asset, interval, maxdict)
	time.sleep(1)
	candles = Iq.get_realtime_candles(asset, interval)
	global ticks
	for candle in candles:
		cand = candles[candle]
		cd_handle = {}
		if "open" in cand:
			cd_handle['open'] = cand["open"]
			cd_candle['high'] = candle["max"]
			cd_candle['low'] = candle["min"]
			cd_candle['close'] = candle["close"]
			cd_handle['created_at'] = dt.datetime.fromtimesstamp(candle["from"]).isoformat()
			cd_handle['timestamp'] = candle["from"]
			cd_handle['volume'] = candle["volume"]
			if any(str(tick['created_at']) == str(cd_handle['created_at']) for tick in ticks):
				pass
			else:
				ticks.append(cd_handle)
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
