---
title: Executar etapas do Windows PowerShell no SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: f25f7549-c9b3-4618-85f2-c9a08adbe0e3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d9034e88276192c14eb8d7008ced10b7041e40c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64478547"
---
# <a name="run-windows-powershell-steps-in-sql-server-agent"></a>Executar etapas do Windows PowerShell no SQL Server Agent

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Use o SQL Server Agent para executar scripts do SQL Server PowerShell nas horas agendadas.  
  
**Para executar o PowerShell no SQL Server Agent, usando:**  [Etapa de trabalho do PowerShell](#PShellJob), [Etapa de trabalho de prompt de comando](#CmdExecJob)  
  
> [!IMPORTANT]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).


Existem vários tipos de etapas de trabalho do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent. Cada tipo está associado a um subsistema que implementa um ambiente específico, como um agente de replicação ou ambiente de prompt de comando. Você pode codificar os scripts do Windows PowerShell e usar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent para incluir os scripts em trabalhos que são executados em horários programados ou em resposta a eventos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Scripts do Windows PowerShell podem ser executados usando uma etapa de trabalho de prompt de comando ou uma etapa de trabalho do PowerShell.  

- Use uma etapa de trabalho do PowerShell para fazer com que o subsistema do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent execute o utilitário **sqlps** , que inicia o PowerShell e importa o módulo **sqlps** .

- Use uma etapa de trabalho de prompt de comando para executar o PowerShell.exe e especifique um script que importa o módulo **sqlps** .

### <a name="LimitationsRestrictions"></a> Cuidado sobre o consumo de memória

Cada etapa de trabalho do Agente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que executa o PowerShell com o módulo **sqlps** inicia um processo, que consome aproximadamente **20 MB** de memória. A execução de um grande número de etapas de trabalho concorrentes do Windows PowerShell pode afetar o desempenho de forma negativa.  

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="PShellJob"></a> Criar uma etapa de trabalho do PowerShell  
 **Para criar uma etapa de trabalho do PowerShell**  
  
1.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criando trabalhos](../ssms/agent/create-jobs.md).  
  
2.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
3.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
4.  Na lista **Tipo** , clique em **PowerShell**.  
  
5.  Na lista **Executar como** , selecione a conta proxy com as credenciais que o trabalho usará.  
  
6.  Na caixa **Comando** , digite a sintaxe do script PowerShell que será executada para a etapa de trabalho. Como alternativa, clique em **Abrir** e selecione um arquivo que contenha a sintaxe de script.  
  
7.  Clique na página **Avançado** para definir as seguintes opções de etapa de trabalho: a ação a tomar em caso de êxito ou falha da etapa, quantas vezes o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent deve tentar executar a etapa e com que frequência.  
  
##  <a name="CmdExecJob"></a> Criar uma etapa de trabalho de prompt de comando  
 **Para criar uma etapa de trabalho CmdExec**  
  
1.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criando trabalhos](../ssms/agent/create-jobs.md).  
  
2.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
3.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
4.  Na lista **Tipo** , escolha **Sistema operacional (CmdExec)** .  
  
5.  Na lista **Executar como** , selecione a conta proxy com as credenciais que o trabalho usará. Por padrão, etapas de trabalho CmdExec são executadas no contexto da conta do serviço do SQL Server Agent .  
  
6.  Na caixa **Código de saída do processo de um comando bem sucedido** , insira um valor de 0 a 999999.  
  
7.  Na caixa **Comando** , digite powershell.exe com parâmetros que especificam o script do PowerShell a ser executado.  
  
8.  Clique na página **Avançado** para definir opções para a etapa de trabalho, como a ação a tomar em caso de êxito ou falha da etapa, quantas vezes o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent deve tentar executar a etapa e o arquivo onde o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent pode gravar a saída da etapa. Somente membros da função de servidor fixa **sysadmin** podem gravar a saída de etapas de trabalho em um arquivo do sistema operacional.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
