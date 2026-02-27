        text-align: center;
    }import React, { useEffect, useMemo, useState } from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Input } from "@/components/ui/input"; import { Select, SelectContent, SelectItem, SelectTrigger, SelectValue } from "@/components/ui/select"; import { Slider } from "@/components/ui/slider"; import { motion } from "framer-motion"; import { Search } from "lucide-react";

// =============================== // MOCK API (substituir por API real Zap/OLX/VivaReal) // =============================== async function fetchProperties() { // Aqui futuramente você pode integrar API real return [ { id: 1, bairro: "Centro", preco: 180000, aluguel: 1800, tipo: "Apartamento", quartos: 2, cidade: "Belo Horizonte" }, { id: 2, bairro: "Savassi", preco: 450000, aluguel: 4200, tipo: "Apartamento", quartos: 3, cidade: "Belo Horizonte" }, { id: 3, bairro: "Venda Nova", preco: 220000, aluguel: 2000, tipo: "Casa", quartos: 3, cidade: "Belo Horizonte" }, { id: 4, bairro: "Buritis", preco: 350000, aluguel: 3200, tipo: "Apartamento", quartos: 2, cidade: "Belo Horizonte" }, { id: 5, bairro: "Pampulha", preco: 600000, aluguel: 5500, tipo: "Casa", quartos: 4, cidade: "Belo Horizonte" }, ]; }

function calculateROI(preco, aluguel) { return ((aluguel * 12) / preco) * 100; }

function calcularFinanciamento(valorImovel, entrada, jurosAnual, anos) { const valorFinanciado = valorImovel - entrada; const jurosMensal = jurosAnual / 100 / 12; const parcelas = anos * 12;

const parcela = (valorFinanciado * jurosMensal) / (1 - Math.pow(1 + jurosMensal, -parcelas));

return parcela; }

export default function PlataformaImoveis() { const [properties, setProperties] = useState([]); const [search, setSearch] = useState(""); const [tipo, setTipo] = useState("Todos"); const [precoMax, setPrecoMax] = useState([700000]); const [roiMin, setRoiMin] = useState([5]); const [entrada, setEntrada] = useState(50000); const [juros, setJuros] = useState(10); const [anos, setAnos] = useState(30);

// Simulação simples SaaS (controle de acesso) const [isPremium, setIsPremium] = useState(false);

useEffect(() => { fetchProperties().then(setProperties); }, []);

const filtered = useMemo(() => { return properties .map((p) => ({ ...p, roi: calculateROI(p.preco, p.aluguel) })) .filter((p) => p.cidade === "Belo Horizonte" && p.bairro.toLowerCase().includes(search.toLowerCase()) && (tipo === "Todos" || p.tipo === tipo) && p.preco <= precoMax[0] && p.roi >= roiMin[0] ) .sort((a, b) => b.roi - a.roi); }, [properties, search, tipo, precoMax, roiMin]);

return ( <div className="min-h-screen bg-gray-50 p-6"> <motion.div initial={{ opacity: 0, y: -20 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.5 }} className="max-w-7xl mx-auto" > <h1 className="text-3xl font-bold mb-6">Plataforma de Arrecadação Imobiliária - BH</h1>

<div className="mb-4">
      <Button onClick={() => setIsPremium(!isPremium)}>
        {isPremium ? "Modo Premium Ativado" : "Ativar Modo Premium"}
      </Button>
    </div>

    <Card className="p-6 rounded-2xl shadow-md mb-8">
      <div className="grid md:grid-cols-4 gap-4">
        <div className="flex items-center gap-2">
          <Search className="w-4 h-4" />
          <Input
            placeholder="Buscar por bairro..."
            value={search}
            onChange={(e) => setSearch(e.target.value)}
          />
        </div>

        <Select onValueChange={setTipo} defaultValue="Todos">
          <SelectTrigger>
            <SelectValue placeholder="Tipo" />
          </SelectTrigger>
          <SelectContent>
            <SelectItem value="Todos">Todos</SelectItem>
            <SelectItem value="Apartamento">Apartamento</SelectItem>
            <SelectItem value="Casa">Casa</SelectItem>
          </SelectContent>
        </Select>

        <div>
          <p className="text-sm mb-1">Preço máximo: R$ {precoMax[0]}</p>
          <Slider
            defaultValue={[700000]}
            max={700000}
            step={10000}
            onValueChange={setPrecoMax}
          />
        </div>

        <div>
          <p className="text-sm mb-1">ROI mínimo: {roiMin[0]}%</p>
          <Slider
            defaultValue={[5]}
            min={0}
            max={15}
            step={0.5}
            onValueChange={setRoiMin}
          />
        </div>
      </div>
    </Card>

    <div className="grid md:grid-cols-3 gap-6">
      {filtered.map((imovel) => {
        const parcela = calcularFinanciamento(
          imovel.preco,
          entrada,
          juros,
          anos
        );

        const fluxoCaixa = imovel.aluguel - parcela;

        return (
          <motion.div
            key={imovel.id}
            whileHover={{ scale: 1.03 }}
            transition={{ duration: 0.2 }}
          >
            <Card className="rounded-2xl shadow-lg">
              <CardContent className="p-4 space-y-2">
                <h2 className="text-xl font-semibold">
                  {imovel.tipo} - {imovel.bairro}
                </h2>
                <p>Preço: R$ {imovel.preco.toLocaleString()}</p>
                <p>Aluguel estimado: R$ {imovel.aluguel.toLocaleString()}</p>
                <p>ROI: {imovel.roi.toFixed(2)}%</p>

                {isPremium && (
                  <>
                    <p>Parcela estimada: R$ {parcela.toFixed(0)}</p>
                    <p>
                      Fluxo de Caixa: R$ {fluxoCaixa.toFixed(0)}
                    </p>
                  </>
                )}

                <Button className="w-full mt-2">Analisar</Button>
              </CardContent>
            </Card>
          </motion.div>
        );
      })}
    </div>
  </motion.div>
</div>

); }

    header h1 {
        font-size: 2.5rem;
    }

    header p {
        margin-top: 15px;
        font-size: 1.1rem;
        opacity: 0.9;
    }

    .btn {
        display: inline-block;
        margin-top: 25px;
        padding: 12px 25px;
        background: #00c853;
        color: white;
        text-decoration: none;
        border-radius: 30px;
        font-weight: 600;
        transition: 0.3s;
    }

    .btn:hover {
        background: #009624;
    }

    section {
        padding: 60px 20px;
        max-width: 1100px;
        margin: auto;
    }

    .cards {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
        margin-top: 40px;
    }

    .card {
        background: white;
        padding: 25px;
        border-radius: 15px;
        box-shadow: 0 5px 15px rgba(0,0,0,0.05);
        transition: 0.3s;
    }

    .card:hover {
        transform: translateY(-5px);
    }

    .card h3 {
        margin-bottom: 15px;
        color: #2c5364;
    }

    footer {
        background: #111;
        color: white;
        text-align: center;
        padding: 20px;
        margin-top: 40px;
    }

    input, textarea {
        width: 100%;
        padding: 10px;
        margin-top: 10px;
        border-radius: 8px;
        border: 1px solid #ccc;
    }

    form button {
        margin-top: 15px;
        padding: 10px 20px;
        background: #2c5364;
        color: white;
        border: none;
        border-radius: 20px;
        cursor: pointer;
    }

    form button:hover {
        background: #203a43;
    }
</style>

</head>
<body><header>
    <h1>Finanças Inteligentes</h1>
    <p>Aprenda a organizar sua vida financeira e conquistar liberdade financeira</p>
    <a href="#conteudos" class="btn">Ver Conteúdos</a>
</header><section id="conteudos">
    <h2>Principais Conteúdos</h2>
    <div class="cards">
        <div class="card">
            <h3>📊 Controle Financeiro</h3>
            <p>Aprenda a organizar seus gastos e sair do vermelho com métodos simples.</p>
        </div>
        <div class="card">
            <h3>💰 Renda Extra</h3>
            <p>Ideias práticas para aumentar sua renda e acelerar seus objetivos.</p>
        </div>
        <div class="card">
            <h3>📈 Investimentos</h3>
            <p>Primeiros passos para investir com segurança mesmo começando do zero.</p>
        </div>
    </div>
</section><section>
    <h2>Baixe meu eBook gratuito</h2>
    <p>Em breve disponível: Guia prático para organizar sua vida financeira.</p>
    <a href="#contato" class="btn">Quero Receber</a>
</section><section id="contato">
    <h2>Entre em Contato</h2>
    <form>
        <input type="text" placeholder="Seu nome" required>
        <input type="email" placeholder="Seu e-mail" required>
        <textarea rows="4" placeholder="Sua mensagem"></textarea>
        <button type="submit">Enviar</button>
    </form>
</section><footer>
    <p>© 2026 Wilian Alves - Todos os direitos reservados</p>
</footer></body>
</html>
