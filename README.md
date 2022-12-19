# concrete-retaining-wall
Muro de Contenção em Concreto

Verificação da estabilidade quanto ao tombamento, escorregamento e ruptura da fundação
* Perfil trapezoidal, 1 solo, sem nível d'água - PT1S0NA

![image](https://user-images.githubusercontent.com/71474825/208473759-571260f0-cdfb-4ac0-8055-6168918c23aa.png)

Exemplo:

```
# Características do muro
y_w = 25 # peso específico do material kN/m3
h = 6.5 # m
b = 3.8 # m
b0 = 0.8 # m
d = 0 # m

# Características do solo
y_nat = 16 # kN/m3
phi = 30 # °
c = 0 # kPa

ka = np.tan(np.radians(45-(phi*0.5)))**2 # Fator de empuxo ativo do solo
kp = np.tan(np.radians(45+(phi*0.5)))**2 # Fator de empuxo passivio do solo

f = np.tan(np.radians(phi)) # Fator de atrito da fundação
q_adm = 300 # Tensão de ruptura da fundação em kN/m2

# Fatores de segurança mínimos
FSt_adm = 1.5
FSe_adm = 1.5
FSr_adm = 2.5
```

Resultado:
```
Altua Crítica = 0.0 m
Estabilidade ao tombamento FS = 3.81 ≥ 1.5 - Estável
Estabilidade ao escorregamento FS = 1.92 ≥ 1.5 - Estável
Estabilidade à ruptura da fundação FS = 2.76 ≥ 2.5 - Estável
```
