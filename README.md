Aqui está o diagrama visual, seguido do mapa de contexto completo para o TP3.

<img width="945" height="615" alt="Diagrama" src="https://github.com/user-attachments/assets/ad555790-0098-4b71-9f3c-03b5bdf5e05a" />

---

## Lista de Bounded Contexts

**1. Serviços Agendados** — *Subdomínio principal*
Responsável por organizar atendimentos para serviços ofertados que dependem de horário, como consultas veterinárias, banho, tosa e passeios. Aqui ficam regras de disponibilidade, reserva, conflitos de agenda e distribuição de horários. *Justificativa: é uma parte central da experiência do cliente e interfere com muitos serviços únicos da plataforma.*

**2. Pagamentos** — *Subdomínio genérico*
Cuida do processamento de pagamentos da plataforma, incluindo pagamentos únicos, recorrências, confirmação de transações.
*Justificativa: normalmente utiliza soluções já existentes no mercado.*

**3. Assinaturas** — *Subdomínio principal*
Gerencia planos recorrentes de produtos ou serviços personalizados para cada pet, definindo frequência de entrega, renovação e preferências do tutor. 
*Justificativa: cria relacionamento contínuo com o cliente e precisa de regras especificamente definidas.*

**4. Passeadores** — *Subdomínio de suporte*
Controla cadastro, disponibilidade e qualificação dos profissionais responsáveis pelos passeios dos animais. 
*Justificativa: sustenta um serviço importante da plataforma, mas com regras mais operacionais do que estratégicas.*

**5. Gestão de Veterinários** — *Subdomínio principal*
Concentra tudo relacionado aos profissionais veterinários: cadastro, disponibilidade para atendimento e emissão de prescrições quando aplicável. 
*Justificativa: É um dos serviços que mais exigem regras específicas de domínio devido à importância ligada ao cliente final.*

**6. E-commerce** — *Subdomínio principal*
Gerencia navegação, carrinho, pedidos e entrega para tutores. 
*Justificativa: é a principal fonte de geração de receita e precisa atender regras comerciais próprias.*

**7. Tipos de Serviço** — *Subdomínio de suporte*
Define e organiza os serviços oferecidos pela plataforma, que serão consumidos pelos serviços agendados. 
*Justificativa: funciona como estrutura de apoio para outros contextos, permitindo padronização e expansão do catálogo de serviços.*

**8. Locações Pet Friends** — *Subdomínio de suporte*
Gerencia unidades, cobertura por região, capacidade operacional e distribuição territorial dos atendimentos e entregas. 
*Justificativa: mantém a operação funcionando em diferentes localidades, mas não representa o principal diferencial do negócio.*

**9. Tutores** — *Subdomínio genérico*
Responsável pelo cadastro e gerenciamento dos responsáveis pelos animais e dos próprios pets, incluindo autenticação e dados básicos de relacionamento com a plataforma. 
*Justificativa: é uma necessidade comum em sistemas desse tipo e normalmente segue padrões já estabelecidos no mercado.*

**10. CFMV (Sistema Externo)** — *Subdomínio genérico*
Conselho Federal de Medicina Veterinária. Valida registro de veterinários. Sistema externo, fora do controle da Pet Friends.

---

## Estratégias de Integração do Contexto de Veterinários

- **Veterinários → CFMV**: *ACL (Anti Corruption Layer)*. O CFMV é um sistema externo com modelo próprio. Deve-se criar uma camada de tradução que isola o domínio interno das mudanças do conselho. A integração é assíncrona (validação periódica ou por evento de cadastro).

- **Veterinários → Catálogo de Produtos (Farmácia)**: relação *Parceria (Partnership)*. A prescrição de remédios exige colaboração bidirecional, Veterinários precisa referenciar o catálogo, e o catálogo pode ter verificações para produtos controlados. 

- **Veterinários → Gestão de Franquias**: *Cliente–Fornecedor*. Franquias informam quais unidades possuem veterinários e suas localizações.---


O contexto de **Veterinários é um contexto consumidor líquido** ele não fornece serviços para outros contextos, mas depende de Agendamento, Franquias e Identidade. A única exceção é a integração com o **Catálogo de Farmácia**, que é uma parceria, ambos se necessitam.

