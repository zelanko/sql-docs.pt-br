---
title: O que &#39; s do SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
caps.latest.revision: 24
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 191fe2e11c43f4c190a87ee52df9ff87c259ea7d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-oracle-oracletosql"></a>O que &#39; s do SSMA para Oracle (OracleToSQL)
Este tópico lista SSMA para alterações do Oracle em cada versão.  

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para Oracle contém as seguintes alterações:  

1.  Adicionado suporte para o SQL Server 2016
2.  Conversão adicional das tabelas de arquivo morto de reversão do Oracle em tabelas temporais do SQL Server
3.  Conversão adicional da política de VPD Oracle conversão em objetos de política do SQL Server (segurança em nível de linha para Oracle)
4.  Menor tempo de carregamento inicial para Oracle
5.  Resolvedor e o analisador aprimorado
6.  Removida a seleção de instalador para .net 2.0
7.  Atualizada a dependência de pacote de extensão do .net 3.5 para o .net 4.0
8.  Fixa "salvar o projeto" e "Abrir projeto" comandos do Console SSMA
9.  Comando fixa "securepassword" para o Console do SSMA
10. Fixa a contagem de objetos para o carregamento inicial
11. Fixa a conversão de tipos de dados de caractere para Oracle
12. Correção do bug nas configurações globais
  
## <a name="march-2016"></a>Março de 2016  
A versão de visualização de março de 2016 do SSMA para Oracle contém as seguintes alterações:  
  
1.  Suporte à migração para o SQL Server 2016  
  
2.  Suporte para migrar Oracle linha nível de segurança (com algumas limitações)  
  
3.  Suporte para a migração de tabelas do Oracle na memória para o repositório de coluna do SQL Server  
  
## <a name="january-2016"></a>Janeiro de 2016  
Janeiro de 2014 a versão de manutenção do SSMA para Oracle contém as seguintes alterações:  
  
1.  Adicionado suporte para índices clusterizados  
  
2.  Consultas de esquema lenta Oracle (RFC 5076207) fixas  
  
3.  Fixa se conectar ao Azure do console  
  
4.  Item de Menu de Log de exibição adicionado para o SSMA (RFC 5706203)  
  
5.  Telemetria adicionada  
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA para Oracle contém as seguintes alterações:  
  
1.  Suporte para o banco de dados SQL do Azure  
  
2.  Funcionalidade do pacote de extensão é movido para o esquema para oferecer suporte a banco de dados de SQL do Azure  
  
3.  Suporte para exibições materializadas Oracle  
  
4.  Tabelas com otimização de suporte para a memória do SQL Server 2014  
  
5.  Melhorias de desempenho testado para bancos de dados com mais de 10 mil objetos  
  
6.  Aprimoramentos de interface do usuário para lidar com um grande número de objetos  
  
7.  Realce de esquemas LOB "bem conhecidas"  
  
8.  Melhorias de velocidade de conversão  
  
9. Mostrar contagens de objetos na interface do usuário  
  
10. Redução de tamanho de relatório por mais de 25%  
  
11. Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014  
A versão de abril de 2014 do SSMA para Oracle contém as seguintes alterações:  
  
1.  Adicionado suporte do MS SQL Server 2014.  
  
2.  Adicionado suporte de otimização do Oracle 12 e consulta.  
  
3.  Bugs corrigidos sobre conversão para o Azure.  
  
4.  Bugs corrigidos sobre páginas de relatório invisível no Internet Explorer 10.  
  
## <a name="january-2012"></a>Janeiro de 2012  
A versão de janeiro de 2012 do SSMA para Oracle contém as seguintes alterações:  
  
-   Parâmetros de entrada RowType de suporte e RecordType adotou o padrão NULL.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA para Oracle contém as seguintes alterações:  
  
-   Suporte para conversão de sequência de Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] gerador de sequência do "Denali".  
  
-   Melhor relatórios de erros durante a migração de dados.  
  
-   Melhor conversão de instrução usar palavras reservadas.  
  
-   Melhor conversão implícita do valor de data em uma função.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA para Oracle contém as seguintes alterações:  
  
-   Consolidados produto "SSMA para Oracle", que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Suporte de conexão e a migração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Avançado mecanismo para migração de dados do lado cliente, dando suporte a migração paralela de dados.  
  
-   Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
  
-   Compatibilidade com versões anteriores de projetos criados por versões anteriores do SSMA (v 4.0 e v 4.2).  
  
-   SSMA para Oracle v 5.0 produto pode ser instalado lado a lado (SxS) com as versões mais antigas do SSMA (v 4.0 e v 4.2).  
  
-   Suporte para tipos definidos pelo usuário (inclui o subtipo, VARRAY, tabela ANINHADA, tabela de objetos e modo de exibição do objeto) e seus usos em blocos de PL/SQL com mensagens de erro especial.  
  
## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA para Oracle contém as seguintes alterações:  
  
-   Suporte para migração para o SQL Server 2008 R2  
  
-   Novo aplicativo de Console SSMA para execução de linha de comando  
  
-   Suporte para migração de dados usando os mecanismos de migração de dados do lado do cliente e do lado do servidor  
  
-   Suporte para a instrução "SELECT personalizado" na migração de dados  
  
-   Suporte para a migração do Oracle 11g R2  
  
## <a name="june-2008"></a>Junho de 2008  
A versão de junho de 2008 do SSMA para Oracle contém as seguintes alterações:  
  
-   Melhorias no relatório de avaliação foram concluídas. Ela inclui informações adicionais sobre sinônimos, origem bruto para objetos analisável, painéis e remoção de logotipo do SQL Server e conservação de layout.  
  
-   Melhorias na conversão do objeto:  
  
    -   Pacotes DBMS_LOB, conversão de DBMS_SQL adicionado.  
  
    -   Une conversão revisado.  
  
    -   Modificação de conversão de registros e coleções, agora a conversão de registros em casos simples lançados por meio de variáveis separadas para cada campo.  
  
    -   Aperfeiçoamentos de implementação de registros e coleções.  
  
    -   Funções de agregação em janela adicionadas.  
  
    -   Cláusula ROLLUP/cubo adicionada.  
  
    -   Aperfeiçoamento de NEXTVAL/CURVAL.  
  
    -   Colunas de agrupamento na cláusula SET, conjuntos de agrupamentos e a ID de agrupamento foram adicionadas.  
  
    -   MESCLE instrução adicionada.  
  
    -   Suporte de novos tipos de data/hora e a conversão de registros e coleções como tipos de dados CLR adicionados.  
  
-   Foram adicionados novos recursos do avaliador. Tabelas agora podem ser testadas como objetos usando o testador, a ordem de chamada de vários objetos podem ser testados no caso de teste pode ser alterada, usuário pode testar procedimentos e funções com registros e coleções como parâmetros e retornar valores e dependências de um analisador foi adicionado para verificar somente tabelas usaram.  
  
## <a name="august-2007"></a>Agosto de 2007  
A versão de agosto de 2007 do SSMA para Oracle contém as seguintes alterações:  
  
-   Um novo componente TESTER permite criar, gerenciar e executar casos de teste para verificar o código SQL convertido.  
  
-   Conversão de subtipos Oracle, coleções e módulos locais foram adicionadas para o conversor de SQL.  
  
-   Um novo recurso de sincronização permite sincronizar objetos específicos com o banco de dados do SQL Server.  
  
-   Novas opções de conversão adicionadas.  
  
## <a name="april-2007"></a>Abril de 2007  
A versão de abril de 2007 do SSMA para Oracle foi a versão inicial.  
  

