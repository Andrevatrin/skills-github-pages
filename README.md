<!DOCTYPE html>
<html lang="pt-br">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Portfólio Empreendedor</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet" />
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(to right, #f1f5f9, #e1ecf4);
      color: #333;
    }

    header {
      background: linear-gradient(90deg, #007cf0, #00dfd8);
      color: white;
      padding: 40px 20px;
      text-align: center;
      border-bottom: 5px solid #00bcd4;
    }

    header h1 {
      margin: 0;
      font-size: 2.5rem;
    }

    header p {
      font-size: 1.2rem;
    }

    .container {
      max-width: 1100px;
      margin: 30px auto;
      padding: 0 20px;
    }

    form {
      background-color: white;
      padding: 25px;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08);
      margin-bottom: 40px;
      transition: 0.3s;
    }

    form:hover {
      transform: scale(1.01);
    }

    label {
      font-weight: 600;
      margin-top: 10px;
      display: block;
      margin-bottom: 5px;
    }

    input, select {
      width: 100%;
      padding: 12px;
      margin-bottom: 20px;
      border-radius: 10px;
      border: 1px solid #ccc;
      font-size: 1rem;
    }

    input[type="file"] {
      background-color: #f9f9f9;
    }

    button {
      background: linear-gradient(90deg, #007cf0, #00dfd8);
      color: white;
      padding: 12px 25px;
      border: none;
      font-size: 1rem;
      font-weight: bold;
      border-radius: 12px;
      cursor: pointer;
      transition: background 0.3s ease;
      box-shadow: 0 5px 15px rgba(0, 124, 240, 0.3);
    }

    button:hover {
      background: linear-gradient(90deg, #00dfd8, #007cf0);
    }

    .filter-buttons {
      text-align: center;
      margin-bottom: 30px;
    }

    .filter-buttons button {
      margin: 6px;
      padding: 10px 18px;
      border-radius: 30px;
      border: none;
      font-size: 0.9rem;
      background-color: #d0d9e0;
      cursor: pointer;
      transition: all 0.2s ease-in-out;
    }

    .filter-buttons button:hover,
    .filter-buttons button.active {
      background: #007cf0;
      color: white;
    }

    .portfolio {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 25px;
    }

    .card {
      background: white;
      border-radius: 15px;
      box-shadow: 0 6px 16px rgba(0, 0, 0, 0.08);
      overflow: hidden;
      transition: 0.3s ease;
    }

    .card:hover {
      transform: translateY(-5px);
    }

    .card img {
      width: 100%;
      height: 200px;
      object-fit: cover;
    }

    .card-content {
      padding: 18px;
    }

    .card-content h3 {
      margin-top: 0;
      color: #007cf0;
      font-size: 1.2rem;
    }

    .card-content p {
      margin: 5px 0;
      font-size: 0.95rem;
    }

    @media (max-width: 768px) {
      header h1 {
        font-size: 2rem;
      }
    }
  </style>
</head>
<body>

<header>
  <h1>Portfólio de Negócios Locais</h1>
  <p>Cadastre seu negócio, escolha uma categoria e filtre abaixo</p>
</header>

<div class="container">
  <!-- Formulário -->
  <form id="cadastroForm">
    <label for="nome">Nome do Comércio:</label>
    <input type="text" id="nome" required />

    <label for="produto">Nome do Produto:</label>
    <input type="text" id="produto" required />

    <label for="contato">Contato:</label>
    <input type="text" id="contato" required />

    <label for="categoria">Categoria:</label>
    <select id="categoria" required>
      <option value="">Escolha uma categoria</option>
      <option value="comida">Comida</option>
      <option value="roupas">Roupas</option>
      <option value="artesanato">Artesanato</option>
      <option value="serviços">Serviços</option>
      <option value="outros">Outros</option>
    </select>

    <label for="imagem">Foto do Produto:</label>
    <input type="file" id="imagem" accept="image/*" required />

    <button type="submit">Adicionar ao Portfólio</button>
  </form>

  <!-- Filtros -->
  <div class="filter-buttons">
    <button class="filter-btn active" data-filter="all">Todos</button>
    <button class="filter-btn" data-filter="comida">Comida</button>
    <button class="filter-btn" data-filter="roupas">Roupas</button>
    <button class="filter-btn" data-filter="artesanato">Artesanato</button>
    <button class="filter-btn" data-filter="serviços">Serviços</button>
    <button class="filter-btn" data-filter="outros">Outros</button>
  </div>

  <!-- Portfólio -->
  <div class="portfolio" id="portfolio">
    <!-- Cards adicionados aparecem aqui -->
  </div>
</div>

<script>
  const form = document.getElementById('cadastroForm');
  const portfolio = document.getElementById('portfolio');
  const filterButtons = document.querySelectorAll('.filter-btn');

  form.addEventListener('submit', function (e) {
    e.preventDefault();

    const nome = document.getElementById('nome').value;
    const produto = document.getElementById('produto').value;
    const contato = document.getElementById('contato').value;
    const categoria = document.getElementById('categoria').value;
    const imagemInput = document.getElementById('imagem');
    const imagemFile = imagemInput.files[0];

    if (!imagemFile || !categoria) return;

    const reader = new FileReader();
    reader.onload = function (event) {
      const imgSrc = event.target.result;

      const card = document.createElement('div');
      card.className = `card ${categoria}`;

      card.innerHTML = `
        <img src="${imgSrc}" alt="Produto">
        <div class="card-content">
          <h3>${nome}</h3>
          <p><strong>Produto:</strong> ${produto}</p>
          <p><strong>Contato:</strong> ${contato}</p>
          <p><strong>Categoria:</strong> ${categoria.charAt(0).toUpperCase() + categoria.slice(1)}</p>
        </div>
      `;

      portfolio.appendChild(card);
      form.reset();
    };
    reader.readAsDataURL(imagemFile);
  });

  // Filtro
  filterButtons.forEach(btn => {
    btn.addEventListener('click', () => {
      document.querySelector('.filter-btn.active')?.classList.remove('active');
      btn.classList.add('active');

      const filter = btn.getAttribute('data-filter');
      const cards = document.querySelectorAll('.card');

      cards.forEach(card => {
        if (filter === 'all' || card.classList.contains(filter)) {
          card.style.display = 'block';
        } else {
          card.style.display = 'none';
        }
      });
    });
  });
</script>

</body>
</html>
