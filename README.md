# LocalSync — live seat map for one local train

React (Vite) + Flask + SQLite. No login: each visitor gets a temp id like `R-4F2K`.

## Run (two terminals)

**1. Backend**
```
cd backend
pip install -r requirements.txt
python app.py          # http://127.0.0.1:5000
```

**2. Frontend**
```
cd frontend
npm install
npm run dev            # http://localhost:5173
```
Open http://localhost:5173. For other devices on the same Wi-Fi use the "Network" URL Vite prints.

## DSA used (backend/structures.py)
| Concept | Where |
|---|---|
| Hash map | `people`, `seat_map`: O(1) seat/passenger lookup |
| FIFO queue (deque) | `queues[seat]`: standing people, first in line gets the freed seat |
| Min-heap | `exit_heap` (who gets off next), `suggest()` (soonest-free seat) |
| Fenwick tree | `load`: crowd per station, range-add / point-query in O(log n) |
| Interval rule | seat busy `[board, dest)`; a stander needs `dest > free_at` |

Demo: use "Next station" to move the train; seats free up and standers get promoted. "Reset demo" reseeds dummy passengers.
