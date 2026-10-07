# Página de manutenção do portal, deixada pelo fornecedor anterior.
# Deveria mostrar o aviso "Voltamos em breve" na porta 80 do container.
# Página de manutenção corrigida
FROM nginx:1.27-alpine
WORKDIR /usr/share/nginx/html
COPY site/ .
EXPOSE 80