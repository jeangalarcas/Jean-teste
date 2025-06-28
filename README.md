#!/bin/bash

# Clone o repositório
git clone https://github.com/jeangalarcas/Jean-teste.git
cd Jean-teste

# Crie o index.html com conteúdo correto
cat > index.html << 'EOL'
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GeoImóveis RS/SC</title>
    <!-- Todo o conteúdo do index.html aqui -->
EOL
# ... (coloque todo o conteúdo HTML aqui) ...
echo "</html>" >> index.html

# Crie arquivos essenciais
touch .nojekyll
mkdir -p .github/workflows

cat > .github/workflows/deploy.yml << 'EOL'
name: Deploy GeoImóveis
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    permissions:
      pages: write
      id-token: write
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: '.'
      - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v2
EOL

# Commit e push
git add .
git commit -m "Correção automática completa"
git push origin main
