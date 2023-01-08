# Gravity Retaining Wall

* Gravity containment wall

Checking the stability of tipping, slipping and breaking the foundation

* Muro de contenção de gravidade

Verificação da estabilidade quanto ao tombamento, escorregamento e ruptura da fundação

![image](https://user-images.githubusercontent.com/71474825/211171872-78c429ec-bd13-4fbc-a361-d8923299f0d6.png)

Exemplo:

```
# ------------------------------Rotina de cálculo-------------------------------

# Características do muro
y_w = 24 # peso específico do material kN/m3
h = 3 # m
b = 0.6 # m
b0 = 0.3 # m
b1 = 0 # m
b2 = 0 # m
d = 0.5 # m

# Características do solo
y_nat = 20 # kN/m3
phi = 30 # °
c = 10 # kPa

f = np.tan(np.radians(phi)) # Fator de atrito da fundação
q_adm = 300 # Tensão de ruptura da fundação em kN/m2

# Esforço Inicial
top_stress = 10

# Fatores de segurança mínimos
FSt_adm = 1.5
FSe_adm = 1.5
FSr_adm = 2.5

# ------------------------------Cálculo dos Elementos---------------------------
W, xw = GravityRetainingWall(h=h,b=b,b0=b0,b1=b1,b2=b2,d=d,y_w=y_w,y_nat=y_nat)

# Empuxo Ativo
Ea, ya = ActiveThrust(
    top_stress=top_stress,
    H=h+d,
    y_nat=y_nat,
    phi=phi,
    c=c
    )

# Empuxo Passivo
Ep, yp = PassiveThrust(
    top_stress=top_stress,
    H=d,
    y_nat=y_nat,
    phi=phi,
    c=c
    )

DesignAnalysis(
    W=W,
    xw=xw,
    b=b+b1+b2,
    AT=Ea,
    yAT=ya,
    PT=Ep,
    yPT=yp,
    f=f,
    q_adm=q_adm,
    FSt_adm=1.5,
    FSe_adm=1.5,
    FSr_adm=2.5,
    logs=True)
```

Resultado:
```
Estabilidade ao tombamento FS = 1.8 ≥ 1.5 - Estável
Estabilidade ao escorregamento FS = 3.66 ≥ 1.5 - Estável
Estabilidade à ruptura da fundação FS = 3.31 ≥ 2.5 - Estável
True
```

Para os seguintes perfis:
* b = b0; b1 > 0; b2 > 0; d > 0 -> Perfil "T" invertido
* b = b0; b1 = 0; b2 > 0; d ≠ 0 -> Perfil "L"
* b = b0; b1 = 0; b2 = 0 -> Perfil Prancha
* b > b0; b1 = 0; b2 = 0 -> Perfil Trapeizoidal
