
<h2 align="center">Cómo enviar 1atom y perder 9atom al mismo tiempo.</h2>
<h2 align="center">HowTo send 1atom and burn 9atom at the same time.</h2>

#Primero hay que compilar una versión especial de gaiacli
#Firtly you have to compile a special version of gaiacli

Pasos:
Compiling steps:

```
mkdir -p ~/go/src/github.com/cosmos
cd ~/go/src/github.com/cosmos
git clone https://github.com/cosmos/cosmos-sdk
cd cosmos-sdk
git fetch --tags
git checkout bez/limited-multisend-cmd
make update_tools
make get_vendor_deps
make install
```

```
gaiacli version --long
```

# It should match this:

```
gaiacli version --long
cosmos-sdk: 0.33.0-1-ga08822d
git commit: a08822d6b6afc1cd7b927d20e614f6c1a90736a6
vendor hash: 81cd66597752534f2724035e5444bf2394d32623
build tags: netgo ledger
go version go1.11.5 linux/amd64
```

# Suponemos que ya tienes tu wallet importada en tu nodo.
# It is supposed you have imported the wallet in your node.

# Creamos la transacción especial que destruye 9atom y envía 1atom
# Create de special TX that burns 9atoms and send 1atom

```
gaiacli tx multisend <cosmos address  --from=YourKey --fees=5000uatom --chain-id=cosmoshub-1 > unsigned_limited_multisend.json
```

# Firmamos la transacción
# Sign the TX

```
gaiacli tx sign unsigned_limited_multisend.json --fees=5000uatom --from=YourKey --validate-signatures --chain-id=cosmoshub-1 > signed_limited_multisend.json
```

# Enviamos la transacción a la red
# Sent the TX to the network

```
gaiacli tx broadcast signed_limited_multisend.json --fees=5000uatom --from=YourKey --memo=MushoBetis --chain-id=cosmoshub-1
```

# Es todo
# End
