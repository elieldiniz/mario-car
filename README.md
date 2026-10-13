# Mario's Auto Sales & Rentals — Site

Site institucional com vitrine de carros usados para a **Mario's Auto Sales & Rentals**, revenda independente em Dracut, Massachusetts (EUA), e um painel administrativo simples para a loja cadastrar os carros.

O objetivo do site é um só: **mostrar os carros disponíveis e levar o cliente a chamar a loja no WhatsApp.** Não há venda online, financiamento, reserva nem login de cliente.

---

## Sumário

1. [Cliente](#1-cliente)
2. [Escopo](#2-escopo)
3. [Mockups](#3-mockups)
4. [Site público](#4-site-público)
5. [Painel administrativo](#5-painel-administrativo)
6. [Regras de negócio](#6-regras-de-negócio)
7. [Modelo de dados](#7-modelo-de-dados)
8. [Stack](#8-stack)
9. [Estrutura do projeto](#9-estrutura-do-projeto)
10. [Rotas](#10-rotas)
11. [Instalação local](#11-instalação-local)
12. [Variáveis de ambiente](#12-variáveis-de-ambiente)
13. [Deploy](#13-deploy)
14. [Identidade visual](#14-identidade-visual)
15. [Requisitos legais (EUA / Massachusetts)](#15-requisitos-legais-eua--massachusetts)
16. [SEO](#16-seo)
17. [Acessibilidade](#17-acessibilidade)
18. [Pendências com o cliente](#18-pendências-com-o-cliente)
19. [Fora do escopo (v2)](#19-fora-do-escopo-v2)

---

## 1. Cliente

| Item | Valor |
| --- | --- |
| Nome | Mario's Auto Sales & Rentals |
| Endereço | 1336 Merrimack Ave, Dracut, MA 01826, EUA |
| Telefone / WhatsApp | (978) 417-4036 |
| Tipo | Revenda independente de carros usados |
| Público | Moradores de Dracut, Lowell e região (inclui comunidade brasileira e latina) |
| Idioma do site | Inglês |
| Moeda / unidades | USD, milhas (mi) |
| Contato do projeto | João Antônio |

---

## 2. Escopo

**Dentro do escopo (v1)**

- Página única (one-page) com topo, busca, marcas, estoque, informações da loja e rodapé.
- Detalhe do carro em janela (modal) com fotos, specs e botão de WhatsApp.
- Filtros por marca, carroceria e preço máximo.
- Botão "Show more cars" (paginação incremental).
- Páginas legais: Privacy Policy, Terms of Use e Accessibility.
- Painel admin com 3 telas: **Cars**, **Categories** e **Store info**.

**Decisões já tomadas com o cliente**

- Só inglês (sem versão em português ou espanhol).
- Só venda de carros (a oficina não entra no site).
- Sem menu de navegação no header, sem botão de WhatsApp no header.
- Sem número de estoque (Stock #), sem VIN visível, sem controle de estoque.
- Sem "Test drive" e sem "Text us": o único canal de contato no carro é o WhatsApp.
- Sem carrossel no topo: um texto fixo sobre a foto do pátio.
- Tema claro fixo (sem modo escuro).

---

## 3. Mockups

| Mockup | Link |
| --- | --- |
| Site público (clicável) | https://claude.ai/artifact/9gaT545r3iuFsaFHDXEHvv |
| Painel admin (clicável) | https://claude.ai/artifact/N53RYp43eGtVyakdEbmabu |
| Briefing | https://claude.ai/code/artifact/a106a77b-5e64-4da2-b35d-e106d2bdde65 |

Os mockups usam dados e fotos de exemplo. Algumas fotos são de outras revendas e devem ser trocadas pelas fotos reais do pátio do Mario antes de publicar.

---

## 4. Site público

Página única, mobile-first. Seções na ordem em que aparecem:

### 4.1 Header (fixo no topo)

- Logo oficial (PNG sem fundo) à esquerda.
- À direita: endereço, horário e telefone em destaque, cada um com ícone.
- No celular: só logo + telefone.
- Faixa vermelha de 3px embaixo do header.

### 4.2 Hero

- Foto aérea do pátio ocupando todo o fundo, com sombra escura para o texto ficar legível.
- Texto centralizado:
  - Etiqueta: `Used cars · Dracut, MA`
  - Título: `Quality used cars. Prices that make sense.`
  - Subtítulo: `A local, family-run lot where you get a good car and a straight answer.`
  - Botão: `Browse our cars` → rola até o estoque.
- No celular: foto em cima, texto embaixo.

### 4.3 Busca

- Desktop: barra flutuante com **Make**, **Body type**, **Max price** e botão **Search**.
- Celular: só **Body type** e **Max price**, lado a lado, aplicando o filtro ao mudar (a marca fica nos botões da seção seguinte).

### 4.4 Shop by make

- Um botão por categoria cadastrada no admin, na ordem definida lá, com a quantidade de carros ativos.
- Botão `All` primeiro.
- Marca selecionada fica vermelha.
- Categoria sem carro ativo não aparece.
- No celular: uma linha só, com rolagem horizontal.

### 4.5 On the lot (estoque)

- Grade de cards, 12 por vez + botão `Show more cars` e texto `Showing X of Y cars`.
- Card do carro:
  - Foto de capa (zoom leve no hover) + selo `Price drop` quando marcado.
  - Botão `View details` sobre a foto (visível no hover; sempre visível no celular).
  - Nome, versão.
  - Etiquetas: milhas, câmbio, tração.
  - Preço + `incl. dealer fees`.
  - Botão verde `Ask about this car` (WhatsApp com mensagem pronta).
- Estado vazio quando o filtro não encontra nada, sugerindo chamar no WhatsApp.

### 4.6 Detalhe do carro (modal)

- Galeria de fotos.
- Nome, versão, milhas, preço e aviso `Includes dealer fees. Plus tax, title & registration.`
- Specs: motor (opcional), câmbio, tração, carroceria, cor.
- Faixa da garantia de Massachusetts calculada pelas milhas (ver §6.3).
- Descrição.
- Botão `WhatsApp about this car` fixo no rodapé do modal.

### 4.7 Bloco de confiança

Três colunas: preços claros, garantia de usados de Massachusetts, loja local e familiar.

### 4.8 Trade-in

Faixa vermelha `Trading in? Get a cash offer.` com botão `Value my car` → WhatsApp com mensagem pronta.

### 4.9 Visit the lot

- Endereço, telefone e horários (vindos de Store info).
- Mapa do Google incorporado (iframe) com botão `Open in Google Maps`.

### 4.10 Rodapé

- Logo, aviso legal de preço, links para Privacy Policy, Terms e Accessibility, copyright.

### 4.11 Mensagens de WhatsApp

Todos os links usam `https://wa.me/<numero>?text=<mensagem>`, com o número vindo de Store info.

| Origem | Mensagem |
| --- | --- |
| Card / detalhe do carro | `Hi Mario, is the {title} {trim} still available?` |
| Trade-in | `Hi Mario, I'd like an offer on my car.` |

---

## 5. Painel administrativo

Acesso em `/admin`. Pensado para ser usado **pelo celular**, no pátio. Idioma: inglês (pode ser trocado para pt-BR, o Filament já tem tradução).

Usuários: 1 ou 2 (Mario e João). Sem níveis de permissão na v1.

### 5.1 Cars

**Lista**
- Foto, nome, versão, milhas, categoria, quantidade de fotos, selos (`Price drop`, `Hidden from site`) e preço.
- Interruptor **On site / Hidden** direto na lista.
- Busca por nome e filtro por categoria.
- Editar e excluir (com confirmação).

**Formulário (criar / editar)**

| Campo | Tipo | Obrigatório | Observação |
| --- | --- | --- | --- |
| Photos | upload múltiplo | sim, para publicar | Reordenáveis; a 1ª é a capa |
| Category | select | sim | Lista de Categories |
| Name | texto | sim | Ex.: `2019 Jeep Compass` |
| Version | texto | não | Ex.: `Limited 4x4` |
| Price | número (USD) | sim, para publicar | Já com as taxas da loja |
| Mileage | número | não | Em milhas |
| Body type | select | sim | `SUV`, `Car`, `Truck` |
| Transmission | select | sim | `Automatic`, `Manual` |
| Drivetrain | select | sim | `FWD`, `RWD`, `AWD`, `4WD` |
| Color | texto | não | |
| Description | texto longo | não | Poucas linhas |
| Show on website | interruptor | — | Liga/desliga no site |
| "Price drop" badge | interruptor | — | Mostra o selo no card |

Ao lado do formulário há uma prévia de como o card vai aparecer no site.

### 5.2 Categories

- Lista com nome e quantidade de carros.
- Adicionar, renomear, mudar ordem (setas) e excluir.
- A ordem aqui é a ordem dos botões `Shop by make` no site.

### 5.3 Store info

Formulário único (sem lista):

- WhatsApp number
- Phone
- Hours: Mon–Fri, Saturday, Sunday (texto livre, ex.: `Closed`)
- Address: street, city, state, ZIP

Usado no header, em Visit the lot, no rodapé, no mapa e em todos os botões de WhatsApp.

---

## 6. Regras de negócio

### 6.1 Publicação

- Um carro só aparece no site se `is_active = true`.
- Não é possível ativar um carro **sem preço** ou **sem pelo menos uma foto** (validação no formulário e no interruptor da lista).
- Vendeu → desligar `Show on website`. Não é preciso excluir.

### 6.2 Categorias

- Não é possível excluir uma categoria que ainda tem carros.
- A contagem pública (`Jeep 4`) considera só carros ativos.
- Categoria sem carros ativos não aparece no site.

### 6.3 Garantia de usados de Massachusetts

Calculada automaticamente pela milhagem e exibida no detalhe do carro (fonte: Used Vehicle Warranty Law, M.G.L. c. 90 § 7N¼):

| Milhas | Garantia |
| --- | --- |
| menos de 40.000 | 90 dias ou 3.750 milhas |
| 40.000 a 79.999 | 60 dias ou 2.500 milhas |
| 80.000 a 124.999 | 30 dias ou 1.250 milhas |
| 125.000 ou mais | sem garantia legal |

Vale para carros acima de US$ 700. Implementar como método no model:

```php
public function maWarranty(): ?string
{
    return match (true) {
        $this->mileage < 40_000  => '90 days or 3,750 miles',
        $this->mileage < 80_000  => '60 days or 2,500 miles',
        $this->mileage < 125_000 => '30 days or 1,250 miles',
        default                  => null,
    };
}
```

### 6.4 Preço

- O preço cadastrado **já inclui todas as taxas da loja** (doc fee etc.). Impostos, título e registro ficam de fora e são avisados no site.
- Nunca condicionar o preço anunciado a financiamento.

### 6.5 Paginação

- 12 carros por carga; `Show more cars` soma mais 12.
- Ao mudar filtro, volta para os 12 primeiros.
- Ordem padrão: mais recentes primeiro (`created_at desc`).

---

## 7. Modelo de dados

```
users
  id, name, email, password, timestamps

categories
  id
  name            string, unique
  sort_order      unsigned int, default 0
  timestamps

cars
  id
  category_id     FK → categories (restrict on delete)
  title           string          // "2019 Jeep Compass"
  trim            string, null    // "Limited 4x4"
  slug            string, unique  // "2019-jeep-compass-limited-4x4-12"
  price           unsigned int    // em dólares, sem centavos
  mileage         unsigned int, null
  body_type       enum: SUV, Car, Truck
  transmission    enum: Automatic, Manual
  drivetrain      enum: FWD, RWD, AWD, 4WD
  color           string, null
  description     text, null
  is_active       boolean, default false
  price_drop      boolean, default false
  timestamps
  index (is_active, category_id)

media  (spatie/laravel-medialibrary)
  fotos dos carros, coleção "photos", com ordem

settings  (linha única)
  id
  whatsapp        string
  phone           string
  street, city, state, zip
  hours_mon_fri, hours_sat, hours_sun   string
  timestamps
```

Observações:
- `price` e `mileage` como inteiros (sem centavos), formatados na view.
- `settings` com uma linha só; ler via cache (`Cache::rememberForever('settings')`) e limpar no save.
- `slug` gerado no save a partir de `title + trim + id`.

---

## 8. Stack

| Camada | Tecnologia |
| --- | --- |
| Backend | Laravel 11+ (PHP 8.3) |
| Site público | Blade + Livewire 3 (filtros e "Show more" sem recarregar a página) |
| Admin | Filament 3 (painel em `/admin`) |
| Fotos | `spatie/laravel-medialibrary` com conversões WebP (`thumb` 600px, `large` 1600px) |
| Storage | Cloudflare R2 ou S3 (disk `s3`) |
| Banco | MySQL 8 ou PostgreSQL |
| CSS | Tailwind CSS 3 (tokens da §14) |
| Fontes | Google Fonts: Barlow Condensed (títulos), Barlow (texto) |
| Hospedagem | Laravel Cloud |

Pacotes sugeridos:

```bash
composer require livewire/livewire filament/filament spatie/laravel-medialibrary filament/spatie-laravel-media-library-plugin league/flysystem-aws-s3-v3
```

---

## 9. Estrutura do projeto

```
app/
  Filament/
    Resources/
      CarResource.php             # lista + formulário de carros
      CategoryResource.php        # categorias com reordenação
    Pages/
      StoreSettings.php           # formulário único de Store info
  Livewire/
    Inventory.php                 # filtros, marcas, "Show more"
    CarDetail.php                 # modal do carro
  Models/
    Car.php                       # scopes active(), maWarranty(), whatsappUrl()
    Category.php                  # scope withActiveCars()
    Setting.php                   # Setting::current()
resources/
  views/
    home.blade.php                # one-page
    legal/
      privacy.blade.php
      terms.blade.php
      accessibility.blade.php
    components/
      car-card.blade.php
      header.blade.php
      footer.blade.php
database/
  migrations/
  seeders/
    CategorySeeder.php
    SettingSeeder.php
    DemoCarSeeder.php             # só para ambiente local
```

---

## 10. Rotas

| Método | URL | Descrição |
| --- | --- | --- |
| GET | `/` | Site (one-page) |
| GET | `/cars/{slug}` | Detalhe do carro (página própria para SEO e compartilhamento; também abre como modal na home) |
| GET | `/privacy` | Privacy Policy |
| GET | `/terms` | Terms of Use |
| GET | `/accessibility` | Accessibility statement |
| GET | `/sitemap.xml` | Sitemap com home, carros ativos e páginas legais |
| — | `/admin/*` | Painel Filament (login obrigatório) |

Query strings aceitas na home (para links e Google): `?make=jeep&body=suv&max=15000&page=2`.

---

## 11. Instalação local

```bash
git clone <repo> marios-auto && cd marios-auto
composer install
npm install
cp .env.example .env
php artisan key:generate

# banco
php artisan migrate --seed

# usuário do admin
php artisan make:filament-user

# fotos em disco local durante o desenvolvimento
php artisan storage:link

npm run dev
php artisan serve
```

- Site: http://localhost:8000
- Admin: http://localhost:8000/admin

---

## 12. Variáveis de ambiente

```dotenv
APP_NAME="Mario's Auto Sales & Rentals"
APP_URL=https://www.mariosautoma.com    # definir domínio
APP_LOCALE=en
APP_TIMEZONE=America/New_York

DB_CONNECTION=mysql
DB_HOST=
DB_DATABASE=
DB_USERNAME=
DB_PASSWORD=

FILESYSTEM_DISK=s3
MEDIA_DISK=s3
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=auto
AWS_BUCKET=
AWS_ENDPOINT=                           # endpoint do R2, se usar Cloudflare
AWS_URL=

CARS_PER_PAGE=12
```

Telefone, WhatsApp, endereço e horários **não** ficam no `.env`: são editados em Store info.

---

## 13. Deploy

Laravel Cloud:

1. Conectar o repositório e criar o ambiente `production`.
2. Banco MySQL gerenciado + bucket de storage.
3. Comandos de deploy:
   ```bash
   php artisan migrate --force
   php artisan optimize
   php artisan filament:optimize
   ```
4. Fila (`queue:work`) para gerar as conversões de imagem da Media Library.
5. Domínio próprio + HTTPS.
6. Cadastrar o site no Google Search Console e enviar `/sitemap.xml`.

---

## 14. Identidade visual

**Logo**: arquivo oficial "Mario's Auto Sales & Rentals" em PNG sem fundo (`public/images/logo.png`). Fica no header (56px de altura no desktop, 42px no celular) e no rodapé. Nunca esticar: sempre `width: auto`.

**Cores**

| Token | Hex | Uso |
| --- | --- | --- |
| `accent` | `#B3121F` | Vermelho da marca: botões, faixa do header, marca selecionada |
| `whatsapp` | `#1A7F45` | Botões de WhatsApp |
| `ink` | `#18161A` | Texto principal |
| `muted` | `#5E5A55` | Texto secundário |
| `bg` | `#F7F6F4` | Fundo da página |
| `surface` | `#FFFFFF` | Cards, header |
| `line` | `#E6E2DD` | Bordas |
| `chip` | `#EFEDEA` | Etiquetas |
| `dark` | `#141216` | Fundo do hero |

**Tipografia**

- Títulos: Barlow Condensed 700–800, caixa alta.
- Texto: Barlow 400–700.

**Interações**

- Card do carro: sobe 4px + sombra, zoom de 6% na foto, título fica vermelho, aparece `View details`.
- Botões de marca: sobem 2px, borda e texto vermelhos, contador vermelho.
- Mapa: zoom leve, botão fica vermelho.
- Respeitar `prefers-reduced-motion` (desligar animações).

---

## 15. Requisitos legais (EUA / Massachusetts)

> Não substitui orientação jurídica. O Mario deve passar os textos legais para um advogado local revisar antes de publicar.

| Tema | Regra | Como o site atende |
| --- | --- | --- |
| Preço anunciado (FTC) | A regra CARS da FTC foi anulada em 2025, mas a FTC continua fiscalizando anúncios com base na lei geral. O preço anunciado deve ser o preço real com todas as taxas da loja. | Preço com taxas incluídas, aviso no card, no detalhe e no rodapé |
| Garantia de usados (MA) | Dealer deve dar garantia escrita por faixa de milhagem | Faixa de garantia calculada no detalhe do carro + citação nos Terms |
| Buyers Guide (FTC Used Car Rule) | Guia afixado no carro físico | Fora do site; os dados do site devem bater com o guia |
| Acessibilidade (ADA) | Revendas são alvo de processos por site inacessível | WCAG 2.1 AA + página Accessibility com contato |
| Privacidade | Leis estaduais de privacidade | Página Privacy Policy |

---

## 16. SEO

- `<title>` e meta description da home: `Used Cars in Dracut, MA | Mario's Auto Sales & Rentals`.
- Página própria por carro (`/cars/{slug}`) com título `2019 Jeep Compass Limited 4x4 for sale in Dracut, MA`.
- Schema.org:
  - `AutoDealer` na home (nome, endereço, telefone, horários vindos de Store info).
  - `Car` em cada carro (nome, preço, milhagem, câmbio, cor, imagem).
- `sitemap.xml` e `robots.txt`.
- Imagens com `alt` descritivo (`White 2018 Jeep Compass`).
- Criar e manter o **Google Business Profile** da loja (hoje ela quase não aparece online).

---

## 17. Acessibilidade

- Contraste mínimo 4.5:1 no texto.
- Todos os botões são `<button>` ou `<a>` reais, com área de toque ≥ 44px.
- Botões só de ícone com `aria-label`.
- Fotos com `alt`; imagens decorativas com `alt=""`.
- Modal com foco preso, `Esc` fecha e o foco volta ao card de origem.
- Navegação completa por teclado com foco visível.
- Página `/accessibility` com telefone e endereço para pedir ajuda.

---

## 18. Pendências com o cliente

- [ ] Horário real de funcionamento (o mockup usa horários de exemplo).
- [ ] Confirmar qual número tem WhatsApp. A prefeitura de Dracut lista também (978) 307-6701.
- [ ] Fotos reais do pátio, incluindo uma foto aérea ou do alto para o topo do site.
- [ ] Fotos reais dos carros (as do mockup são de exemplo, algumas com placas de outras revendas).
- [ ] Domínio: o cliente já tem? Sugestões a verificar: `mariosautoma.com`, `mariosautodracut.com`.
- [ ] O logo diz "& Rentals": o aluguel de carros entra no site?
- [ ] Valor da doc fee, para garantir que está somado aos preços.
- [ ] Revisão dos textos legais por advogado local.
- [ ] Admin em inglês ou português?

---

## 19. Fora do escopo (v2)

- Importar estoque por CSV de sistemas como DealerCenter ou Frazer.
- Publicação automática no Facebook Marketplace / Google Vehicle Listings.
- Formulário de contato e trade-in salvando leads no admin.
- Contagem de cliques no WhatsApp por carro.
- Página de aluguel (se "Rentals" for confirmado).
- Mais usuários com níveis de permissão.