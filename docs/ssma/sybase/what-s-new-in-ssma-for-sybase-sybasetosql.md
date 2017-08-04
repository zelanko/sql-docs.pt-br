---
title: O que &#39; s do SSMA for Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2be0cf8d-6dbe-443a-abbd-036249922205
caps.latest.revision: 21
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9d97e03212e6985ce9d506774bfff0aa2f4ec8d1
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="what39s-new-in-ssma--for-sybase-sybasetosql"></a>O que &#39; s do SSMA for Sybase (SybaseToSQL)
Este tópico lista SSMA para Sybase alterações em cada versão.  

## <a name="may-2016"></a>Maio de 2016  
A versão de maio de 2016 do SSMA for Sybase contém as seguintes alterações:  

1.  Adicionado suporte para o SQL Server 2016
2.  Removida a seleção de instalador para .net 2.0
3.  Atualizada a dependência de pacote de extensão do .net 3.5 para o .net 4.0
4.  Fixa "salvar o projeto" e "Abrir projeto" comandos do Console SSMA
5.  Comando fixa "securepassword" para o Console do SSMA
6.  Fixa a contagem de objetos para o carregamento inicial
7.  Correção do bug nas configurações globais

## <a name="march-2016"></a>Março de 2016  
A versão de visualização de março de 2016 do SSMA for Sybase contém as seguintes alterações:  
  
1.  Suporte à migração para o SQL Server 2016  
  
## <a name="january-2016"></a>Janeiro de 2016  
A versão de manutenção de janeiro de 2016 do SSMA for Sybase contém as seguintes alterações:  
  
1.  Item de Menu de Log de exibição adicionado para o SSMA (RFC 5706203)  
  
2.  Telemetria adicionada  
  
## <a name="july-2014"></a>Julho de 2014  
A versão de julho de 2014 do SSMA for Sybase contém as seguintes alterações:  
  
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
A versão de abril de 2014 do SSMA for Sybase contém as seguintes alterações:  
  
-   Adicionado suporte do MS SQL Server 2014.  
  
-   Bugs corrigidos sobre conversão para o Azure  
  
-   Bugs corrigidos sobre páginas de relatório invisível no Internet Explorer 10.  
  
## <a name="january-2012"></a>Janeiro de 2012  
A versão de janeiro de 2012 do SSMA for Sybase contém as seguintes alterações:  
  
-   Suporte para conversão de gatilho de reversão.  
  
-   Fornecida a correção para converter@ROWCOUNT e @@ERROR na mesma instrução SET.  
  
## <a name="july-2011"></a>Julho de 2011  
A versão de julho de 2011 do SSMA for Sybase contém as seguintes alterações:  
  
-   Melhor relatórios de erros durante a migração de dados.  
  
## <a name="april-2011"></a>Abril de 2011  
A versão de abril de 2011 do SSMA for Sybase contém as seguintes alterações:  
  
-   Produto "SSMA para Sybase" consolidado, o que dá suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali" e o SQL Azure.  
  
-   Suporte de conexão e a migração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] "Denali".  
  
-   Novo recurso para converter e migrar bancos de dados Sybase para o SQL Azure.  
  
-   Avançado mecanismo para migração de dados do lado cliente, dando suporte a migração paralela de dados.  
  
-   Desempenho de migração de dados aprimorada com simples e Bulk logged modelos de recuperação.  
  
-   Bancos de dados Sybase diferencia maiusculas de minúsculas podem ser convertidos e migrados para o SQL Server entre maiusculas e minúsculas corretamente.  
  
-   Suporte para conversão de instruções de junção do Sybase ASE não-ANSI para instruções de junção ANSI do SQL Server foi estendido para excluir e atualizar as instruções.  
  
-   Opções de conectividade adicional para conectar a servidores Sybase ASE usando o provedor do Sybase ASE ODBC e provedores Sybase ASE ADO.Net.  
  
-   Remoção de dependência em um banco de dados separado chamado **SysDB** que contém as funções de emulação do Sybase (instaladas como parte do pacote de extensão).  
  
-   SSMA para Sybase pacote de extensão agora pode ser instalado em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] clusters.  
  
-   Compatibilidade com versões anteriores de projetos criados por versões anteriores do SSMA (v 4.0 e v 4.2).  
  
-   SSMA para Sybase v 5.0 produto pode ser instalado lado a lado (SxS) com as versões mais antigas do SSMA (v 4.0 e v 4.2).  
  
## <a name="july-2010"></a>Julho de 2010  
A versão de julho de 2010 do SSMA for Sybase contém as seguintes alterações:  
  
-   Suporte para migração para o SQL Server 2008 R2  
  
-   Novo aplicativo de Console SSMA para execução de linha de comando  
  
-   Suporte para migração de dados usando os mecanismos de migração de dados do lado do cliente e do lado do servidor  
  
-   Suporte para a instrução "SELECT personalizado" na migração de dados  
  
-   Suporte à migração do Sybase ASE 15.0.3 e 15,5  
  
## <a name="june-2008"></a>Junho de 2008  
A versão de junho de 2008 do SSMA for Sybase contém as seguintes alterações:  
  
-   SSMA Tester adicionado, ele automaticamente testa a conversão do objeto de banco de dados e a migração de dados feitas pelo SSMA. Depois que todas as etapas de migração do SSMA estiverem concluídas, use o SSMA testador para verificar objetos convertidos funcionam da mesma forma e que todos os dados foi transferido corretamente.  
  
-   Conversão de versão anterior do SQL adicionado. Usuário agora pode especificar tabelas temporárias (e outros objetos) declarações para cada procedimento de origem a ser usada na conversão.  
  
-   Melhorias na conversão do objeto:  
  
    -   Une conversão revisado.  
  
    -   Agregações e agregações sem tem que/grupo por cláusulas.  
  
    -   A função de identidade com uma instrução SELECT INTO.  
  
    -   Restrições em cluster e índices em somente dados bloqueados.  
  
    -   Tabelas temporárias criadas pelo SELECT INTO.  
  
    -   Restrições de / índices para tabelas temporárias.  
  
    -   Novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] há suporte para tipos de data/hora de 2008.  
  
    -   Suporte a tipos de dados e conectividade 15.0 Sybase.  
  
## <a name="may-2007"></a>Maio de 2007  
A versão de maio de 2007 do SSMA for Sybase contém as seguintes alterações:  
  
-   Quando você salvar um projeto, carregar o conteúdo do banco de dados é mais rápido.  
  
-   Suporte para comentários inseridos pelo usuário, que o SQL Server formatada de modo SQL.  
  
-   Melhorias na conversão do objeto.  
  
Observe que o arquivo de Ajuda não foi atualizado para esta versão. Para obter mais informações, consulte a seção Notas da documentação mais adiante neste tópico.  
  
## <a name="november-2006"></a>Novembro de 2006  
A versão de novembro de 2006 do SSMA for Sybase contém as seguintes alterações:  
  
-   Novas configurações globais:  
  
    -   Você pode optar por mostrar números de linha na janela do editor.  
  
    -   Você pode configurar o SSMA para perguntar antes de substituir objetos duplicados ou sempre ou nunca substituir objetos duplicados durante a conversão do esquema.  
  
-   Novas opções de conversão permitem que você configure como o SSMA lida com as seguintes situações:  
  
    -   Uma instrução CAST ou CONVERT que contém uma cadeia de caracteres binária  
  
    -   Verifica se há valores nulos em expressões de igualdade  
  
    -   Tabelas de proxy  
  
    -   Números de erro de mensagem do usuário para RAISERROR  
  
    -   Instruções de atualização que contêm identificadores não resolvidos  
  
-   Uma nova opção de migração permite que você especifique como o SSMA deve tratar as datas que estão fora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] intervalo de datas.  
  
-   Um **formatado SQL** definição no **SQL** guia, que formata o código para melhor legibilidade.  
  
-   Correções de bug que incluem o seguinte:  
  
    -   O SSMA agora converte o bloqueio de tabela *tabela* IN {compartilhado | Instruções de modo exclusivo} com a adição de uma dica TABLOCK ou TABLOCKX para a consulta SELECT subsequente na tabela.  
  
    -   As conversões necessárias agora são adicionadas quando tipos binários são usados em expressões de caractere.  
  
    -   Melhorias de desempenho e de memória.  
  
## <a name="july-2006"></a>Julho de 2006  
A versão de julho de 2006 do SSMA for Sybase foi a versão inicial.  
  
## <a name="see-also"></a>Consulte também  
[Guia de Introdução com o SSMA para Sybase &#40; SybaseToSQL &#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  

