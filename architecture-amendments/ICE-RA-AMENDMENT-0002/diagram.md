                    ┌──────────────────────────────────────┐
                    │        Security Management Zone       │
                    │                                      │
                    │   ┌──────────────┐      ┌──────────┐ │
Semantic Plan +     │   │   Engine X   │◄────►│ Storage X│ │
Derived BELIEF      │   │ (Scripts +   │  R/W │ (BELIEF, │ │
(Human/Admin)  ───► │   │  Evidence)   │      │ TRUTH,   │ │
                    │   └──────┬───────┘      │ DELTA,   │ │
                    │          │              │ XRESULT, │ │
                    │          │ controlled   │ DRIFT TS)│ │
                    │          │ submission   └──────────┘ │
                    └──────────┼───────────────────────────┘
                               │
                               ▼
                    ┌──────────────────────────────────────┐
                    │             Model Zone               │
                    │   (separate security zone from       │
                    │    Engine X and Storage X)           │
                    │                                      │
                    │   ┌──────────────┐      ┌──────────┐ │
                    │   │   Model X    │◄───► │ Storage M│ │
                    │   │ (Local LLM)  │  R/W │ (weights,│ │
                    │   └──────▲───────┘      │ taxonomy,│ │
                    │          │ return only  │ cache, ops│ │
                    │          │              │ logs)    │ │
                    │          └──────────────┴──────────┘ │
                    │      (NO PATH to Storage X)          │
                    └──────────────────────────────────────┘


 Zone A                               Controlled Interface                 Zone B
┌──────────────┐                                                           ┌──────────────┐
│ Host A       │                                                           │ Host B       │
│ Ta (nmap)    │                                                           │ Tb (nmap)    │
└──────┬───────┘                                                           └──────┬───────┘
       │ Test traffic                                                             │ Test traffic
       ▼                                                                           ▼
                     ┌──────────────────────────┐
                     │        Firewall F         │
                     │ (Facilitation + Guards)  │
                     └───────────▲──────────────┘
                                 │
                                 │ Read-only logs via admin tap
                                 ▼
                     ┌──────────────────────────┐
                     │        Firewall Fx       │
                     │   (Admin Tap / Control   │
                     └──────────────────────────┘
