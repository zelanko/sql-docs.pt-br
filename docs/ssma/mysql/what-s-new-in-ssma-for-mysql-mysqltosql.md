---
title: O que &#39; s do SSMA para MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 1451a0b0-6713-4d0c-954f-ea3d8fce1d31
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 42706f2ce71fc540d8538f9614f1db17b4f70ea7
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma-for-mysql-mysqltosql"></a>O que &#39; s do SSMA para MySQL (MySQLToSql)
Este tópico lista SSMA para MySQL alterações em cada versão.  

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA para MySQL contém as seguintes alterações:.

1.  Adicionado suporte para o SQL Server 2016
2.  Resolvedor e o analisador aprimorado
3.  Removida a seleção de instalador para .net 2.0
4.  Atualizada a dependência de pacote de extensão do .net 3.5 para o .net 4.0
5.  Padrão fixo BigInt typemapping para MySql
6.  Fixa "salvar o projeto" e "Abrir projeto" comandos do Console SSMA
7.  Comando fixa "securepassword" para o Console do SSMA
8.  Fixa a contagem de objetos para o carregamento inicial
9.  Carregamento de objetos de MsSql fixo
10. Correção do bug nas configurações globais 
 
## <a name="march-2016"></a>Março de 2016  
A versão de visualização de março de 2016 do SSMA para MySQL contém as seguintes alterações:  
  
1.  Suporte à migração para o SQL Server 2016  
  
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA para MySQL contém as seguintes alterações:  
  
1.  Item de Menu de Log de exibição adicionado para o SSMA (RFC 5706203)  
  
2.  Telemetria adicionada  
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA para MySQL contém as seguintes alterações:  
  
1.  Conversão de código de banco de dados do Azure SQL aprimorada  
  
2.  Funcionalidade do pacote de extensão é movido para o esquema para oferecer suporte a banco de dados de SQL do Azure  
  
3.  Melhorias de desempenho testado para bancos de dados com mais de 10 mil objetos  
  
4.  Aprimoramentos de interface do usuário para lidar com um grande número de objetos  
  
5.  Realce de esquemas LOB "bem conhecidas" (para que eles podem ser ignorados na conversão)  
  
6.  Melhorias de velocidade de conversão  
  
7.  Mostrar contagens de objetos na interface do usuário  
  
8.  Redução de tamanho de relatório por mais de 25%  
  
9. Mensagens de erro aprimoradas para construções não analisadas.  
  
## <a name="april-2014"></a>Abril de 2014  
A versão de julho de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
1.  Adicionado suporte do MS SQL Server 2014.  
  
2.  Bugs corrigidos sobre conversão para o Azure  
  
3.  Bugs corrigidos sobre páginas de relatório invisível no Internet Explorer 10.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
-   Suporte para conversão de limite para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] deslocamento "Denali".  
  
-   Melhor relatórios de erros durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA para MySQL contém as seguintes alterações:  
  
-   Instalável do "SSMA para MySQL", que oferece suporte a um único [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" e o SQL Azure.  
  
-   A capacidade de conectar-se [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Avançado mecanismo para migração de dados do lado cliente, dando suporte a migração paralela de dados.  
  
-   Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
  
-   SSMA para a versão do Console do MySQL dá suporte à compatibilidade com versões anteriores. Você poderá abrir os projetos criados por versões anteriores para v 5.0 do SSMA.  
  
-   SSMA para MySQL v 5.0 produto pode ser instalado lado a lado (SxS) com versões anteriores do produto do SSMA.  
  
## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA para MySQL contém os seguintes recursos:  
  
1.  **Aprimoramentos à Interface do usuário:**  
  
    -   Guia de 'modo SQL' para objetos de banco de dados MySQL  
  
    -   Guia "Configurações" para objetos de banco de dados MySQL  
  
    -   Guia de 'Dados' para tabelas de MySQL  
  
    -   Configurações de projeto atualizado na conversão e páginas de migração  
  
    -   'Configurações de migração de dados' no nível de tabela  
  
2.  **Aprimoramentos para se conectar ao SQL Server e MySQL:**  
  
    -   Conectividade SSL no MySQL  
  
    -   Conectividade criptografada no SQL Server  
  
3.  **Aprimoramentos ao Gerenciador de Metabase MySQL:**  
  
    -   Carregar todos os objetos de banco de dados MySQL e seus respectivos guias.  
  
4.  **Aprimoramentos para conversão do objeto:**  
  
    -   Conversão de objetos de Metabase do MySQL – procedimentos, funções, exibições, gatilhos e instruções.  
  
    -   Suporte limitado para tipos de dados espaciais em tabelas.  
  
    -   Opção de converter as funções do MySQL para procedimentos armazenados do SQL Server  
  
    -   Opção de aplicar o mapeamento de modos SQL e o conjunto de caracteres durante a conversão do objeto  
  
5.  **Aprimoramentos para migração de dados:**  
  
    -   Suporte para migração de dados usando os mecanismos de migração de dados do lado do cliente e do lado do servidor  
  
    -   Suporte para a migração de dados espaciais  
  
    -   SQL personalizado para a migração de dados para tabelas  
  
6.  **SSMA para MySQL Console:**  
  
    -   Suporte a recurso de Console para o SSMA para MySQL  
  
    -   Suporte para interface de nível de Script  
  
## <a name="january-2010"></a>Janeiro de 2010  
A versão de janeiro de 2010 do SSMA para MySQL foi a versão inicial. Ele continha os seguintes recursos:  
  
-   Há suporte para migração para o SQL Server local e do SQL Azure.  
  
-   **Recurso de instantâneo:** migração de esquema e dados do MySQL tabelas/índices/restrições.  
  

