# 🎨 ArtConnect - Plataforma de Arte Colaborativa Urbana

👥 Equipe:
    - Maria Fernanda Melo
    - Sara da Cruz
    - João Pedro Gomes

🌟 Resumo do Projeto
O ArtConnect é uma plataforma digital que conecta artistas alternativos urbanos (grafiteiros, muralistas, artistas de rua) com proprietários de espaços que desejam ter arte em suas paredes. A aplicação resolve o problema de artistas que buscam espaços legais para expressar sua arte, enquanto proprietários procuram formas criativas e econômicas de revitalizar seus espaços.
✨ Problema Social que Resolve

Para Artistas: Dificuldade de encontrar espaços legais para criar arte urbana
Para Proprietários: Necessidade de revitalizar espaços de forma criativa e acessível
Para a Comunidade: Transformação de espaços urbanos abandonados em locais culturalmente ricos

🎯 Tema do Projeto
Por que escolhemos este tema?
A cultura urbana e a arte de rua são expressões fundamentais da juventude alternativa moderna. Muitos artistas talentosos enfrentam a criminalização de sua arte por falta de espaços adequados, enquanto muitos espaços urbanos permanecem subutilizados. Nossa plataforma cria uma ponte entre essas necessidades, promovendo:

🎨 Democratização da arte urbana
🏙️ Revitalização de espaços urbanos
🤝 Conexão entre artistas e comunidade
💡 Economia criativa colaborativa

📊 Modelos de Dados (Schemas)
🔐 Usuario (Modelo de Autenticação)
prismamodel Usuario {
  id        String @id @default(auto()) @map("_id") @db.ObjectId
  email     String @unique
  password  String
  nome      String
  tipo      TipoUsuario // ARTISTA ou PROPRIETARIO
  createdAt DateTime @default(now())
  
  // Relacionamentos
  projetos  Projeto[] // Se for artista
  espacos   Espaco[]  // Se for proprietário
}
Justificativa: Modelo central para autenticação e diferenciação entre tipos de usuários (artistas e proprietários de espaços).
🏢 Espaco (Espaços Disponíveis)
prismamodel Espaco {
  id          String @id @default(auto()) @map("_id") @db.ObjectId
  titulo      String
  descricao   String
  endereco    String
  dimensoes   String // ex: "3x2 metros"
  fotos       String[] // URLs das fotos
  disponivel  Boolean @default(true)
  createdAt   DateTime @default(now())
  
  // Relacionamentos
  proprietarioId String @db.ObjectId
  proprietario   Usuario @relation(fields: [proprietarioId], references: [id])
  projetos       Projeto[]
}
Justificativa: Representa os espaços físicos disponíveis para arte. Relaciona-se com usuários proprietários e pode ter múltiplos projetos ao longo do tempo.
🎨 Projeto (Projetos Artísticos)
prismamodel Projeto {
  id          String @id @default(auto()) @map("_id") @db.ObjectId
  titulo      String
  descricao   String
  estilo      EstiloArte // GRAFFITI, MURAL, STENCIL, etc.
  status      StatusProjeto // PROPOSTA, APROVADO, EM_ANDAMENTO, FINALIZADO
  portfolio   String[] // URLs de trabalhos anteriores
  prazo       DateTime
  createdAt   DateTime @default(now())
  
  // Relacionamentos
  artistaId   String @db.ObjectId
  artista     Usuario @relation(fields: [artistaId], references: [id])
  espacoId    String @db.ObjectId
  espaco      Espaco @relation(fields: [espacoId], references: [id])
}
Justificativa: Conecta artistas a espaços específicos, criando a relação central da plataforma. Permite rastreamento do status e histórico dos projetos.
🎭 Enums de Apoio
prismaenum TipoUsuario {
  ARTISTA
  PROPRIETARIO
}

enum EstiloArte {
  GRAFFITI
  MURAL
  STENCIL
  ARTE_DIGITAL
  COLAGEM
  OUTRO
}

enum StatusProjeto {
  PROPOSTA
  APROVADO
  EM_ANDAMENTO
  FINALIZADO
  CANCELADO
}
🔄 Relacionamentos entre Modelos

Usuario → Espaco (1:N): Um proprietário pode ter múltiplos espaços
Usuario → Projeto (1:N): Um artista pode ter múltiplos projetos
Espaco → Projeto (1:N): Um espaço pode hospedar múltiplos projetos ao longo do tempo

⚙️ Comandos para Execução
📦 Instalação de Dependências
bashnpm install prisma @prisma/client typescript ts-node @types/node
🗄️ Configuração do Banco de Dados
bash# Gerar o cliente Prisma
npx prisma generate

# Visualizar o schema no Prisma Studio
npx prisma studio
🚀 Execução do Script de Teste
bash# Executar o script de demonstração
npx ts-node script.ts
📁 Estrutura de Arquivos
projeto/
├── prisma/
│   └── schema.prisma
├── node_modules/
├── script.ts
├── .env
├── package.json
├── tsconfig.json
└── README.md
🎨 Impacto Social Esperado

Legalização da arte urbana: Redução da criminalização através de espaços legais
Revitalização urbana: Transformação de espaços abandonados em pontos culturais
Economia criativa: Geração de renda para artistas alternativos
Cultura comunitária: Fortalecimento da identidade cultural local


"Arte não é o que você vê, mas o que você faz os outros verem." - Edgar Degas
🔗 Tecnologias: Prisma ORM | MongoDB | TypeScript | Node.js
