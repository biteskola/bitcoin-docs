## Como funciona el scrow ("testigo") de Hodl Hodl

1. Comprador y vendedor crean un contrato para el intercambio de x bitcoins por z euros.
2. Se crea una direccion multifirma 2 de 3 donde comprador, vendedor y hodl hodl pueden firmar.
3. Vendedor envia los bitcoins pactados a la direccion multifirma. el servicio hodl hodl comprueba 
que envia los bitcoins pactados, sino no se pasaria al siguiente paso.
4. Comprador envia los euros pactados a la cuenta corrienta del vendedor. Despues, envia su firma.
5. Vendedor confirma que le llegaron los euros pactados. Despues, envia su firma.
6. Se desbloquean los bitcoins con las firmas del comprador y vendedor.

Si alguna de las partes no firma, se crea una disputa donde hodl hodl hace de intermediario. Si comprador 
gana la disputa, hodl hodl firma y se desbloquean los bitcoins con las firmas del comprador y hodl hodl. Si, 
en cambio, el vendedor gana la disputa, genera una nueva tx con las firmas del vendedor y hodl hodl que devuelve
los bitcoins a la direccion del vendedor.

A los vendedores no les interesa caer en disputas, ya que, de esta manera su reputacion empeora.

