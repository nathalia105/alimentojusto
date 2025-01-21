# alimentojusto
import React, { useState } from 'react';
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts';
import { BarChart3, Users, Leaf, Droplet, Thermometer, Wind, Box, Timer, Heart } from 'lucide-react';
import { Card, CardContent, CardHeader, CardTitle } from '@/components/ui/card';

const AlimentoJustoApp = () => {
  const [activeTab, setActiveTab] = useState('dashboard');

  // Dados simulados de monitoramento ambiental
  const environmentalData = [
    { time: '6h', temperatura: 22, umidade: 75, producao: 85 },
    { time: '9h', temperatura: 24, umidade: 70, producao: 88 },
    { time: '12h', temperatura: 27, umidade: 65, producao: 92 },
    { time: '15h', temperatura: 26, umidade: 68, producao: 90 },
    { time: '18h', temperatura: 23, umidade: 72, producao: 87 }
  ];

  const recomendacoesIA = [
    { id: 1, tipo: 'Irrigação', mensagem: 'Reduzir irrigação em 15% - umidade do solo adequada' },
    { id: 2, tipo: 'Colheita', mensagem: 'Colheita ideal em 2 dias para maximizar produtividade' },
    { id: 3, tipo: 'Doação', mensagem: '200kg de excedente previsto - Banco de Alimentos disponível' }
  ];

  return (
    <div className="max-w-4xl mx-auto bg-gray-50 min-h-screen">
      {/* Header */}
      <div className="bg-green-600 text-white p-6">
        <h1 className="text-2xl font-bold">Alimento Justo</h1>
        <p className="text-sm mt-2">IA Contra o Desperdício e Pelo Futuro Verde</p>
      </div>

      {/* Menu Principal */}
      <div className="flex justify-around p-4 bg-white border-b">
        <button 
          className={`flex items-center space-x-2 px-4 py-2 rounded-lg ${activeTab === 'dashboard' ? 'bg-green-100 text-green-600' : 'text-gray-600'}`}
          onClick={() => setActiveTab('dashboard')}
        >
          <BarChart3 className="w-5 h-5" />
          <span>Dashboard</span>
        </button>
        <button 
          className={`flex items-center space-x-2 px-4 py-2 rounded-lg ${activeTab === 'comunidade' ? 'bg-green-100 text-green-600' : 'text-gray-600'}`}
          onClick={() => setActiveTab('comunidade')}
        >
          <Users className="w-5 h-5" />
          <span>Comunidade</span>
        </button>
        <button 
          className={`flex items-center space-x-2 px-4 py-2 rounded-lg ${activeTab === 'doacoes' ? 'bg-green-100 text-green-600' : 'text-gray-600'}`}
          onClick={() => setActiveTab('doacoes')}
        >
          <Heart className="w-5 h-5" />
          <span>Doações</span>
        </button>
      </div>

      {/* Conteúdo Principal */}
      <div className="p-6">
        {/* Métricas Principais */}
        <div className="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
          <Card>
            <CardHeader className="pb-2">
              <CardTitle className="text-sm font-medium text-gray-500">Produção Atual</CardTitle>
            </CardHeader>
            <CardContent>
              <div className="flex items-center">
                <Box className="w-5 h-5 text-green-600 mr-2" />
                <span className="text-2xl font-bold">2.5 ton</span>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader className="pb-2">
              <CardTitle className="text-sm font-medium text-gray-500">Desperdício Evitado</CardTitle>
            </CardHeader>
            <CardContent>
              <div className="flex items-center">
                <Timer className="w-5 h-5 text-orange-600 mr-2" />
                <span className="text-2xl font-bold">450 kg</span>
              </div>
            </CardContent>
          </Card>

          <Card>
            <CardHeader className="pb-2">
              <CardTitle className="text-sm font-medium text-gray-500">Doações Realizadas</CardTitle>
            </CardHeader>
            <CardContent>
              <div className="flex items-center">
                <Heart className="w-5 h-5 text-red-600 mr-2" />
                <span className="text-2xl font-bold">200 kg</span>
              </div>
            </CardContent>
          </Card>
        </div>

        {/* Gráfico de Monitoramento */}
        <Card className="mb-6">
          <CardHeader>
            <CardTitle>Monitoramento em Tempo Real</CardTitle>
          </CardHeader>
          <CardContent>
            <div className="h-64">
              <ResponsiveContainer width="100%" height="100%">
                <LineChart data={environmentalData}>
                  <CartesianGrid strokeDasharray="3 3" />
                  <XAxis dataKey="time" />
                  <YAxis />
                  <Tooltip />
                  <Line type="monotone" dataKey="temperatura" stroke="#ff7300" name="Temperatura" />
                  <Line type="monotone" dataKey="umidade" stroke="#387908" name="Umidade" />
                  <Line type="monotone" dataKey="producao" stroke="#3b82f6" name="Produção" />
                </LineChart>
              </ResponsiveContainer>
            </div>
          </CardContent>
        </Card>

        {/* Recomendações da IA */}
        <Card>
          <CardHeader>
            <CardTitle>Recomendações Inteligentes</CardTitle>
          </CardHeader>
          <CardContent>
            <div className="space-y-4">
              {recomendacoesIA.map(rec => (
                <div key={rec.id} className="flex items-start p-4 bg-gray-50 rounded-lg">
                  <div className="flex-shrink-0">
                    {rec.tipo === 'Irrigação' && <Droplet className="w-6 h-6 text-blue-500" />}
                    {rec.tipo === 'Colheita' && <Leaf className="w-6 h-6 text-green-500" />}
                    {rec.tipo === 'Doação' && <Heart className="w-6 h-6 text-red-500" />}
                  </div>
                  <div className="ml-4">
                    <h4 className="font-semibold">{rec.tipo}</h4>
                    <p className="text-sm text-gray-600">{rec.mensagem}</p>
                  </div>
                </div>
              ))}
            </div>
          </CardContent>
        </Card>
      </div>
    </div>
  );
};
