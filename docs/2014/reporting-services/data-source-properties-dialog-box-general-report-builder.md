---
title: Caixa de diálogo Propriedades da fonte de dados, geral (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10018"
ms.assetid: b956f43a-8426-4679-acc1-00f405d5ff5b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7bedf016dce02928bbd47dbfce60943ec667a824
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109468"
---
# <a name="data-source-properties-dialog-box-general-report-builder"></a>Caixa de diálogo Propriedades da Fonte de Dados, Geral (Construtor de Relatórios)
  Selecione **Geral** na caixa de diálogo **Propriedades da Fonte de Dados** para selecionar uma fonte de dados compartilhada em um servidor de relatório ou para criar ou modificar as informações de conexão de uma fonte de dados inserida no relatório.  
  
 O tipo de credenciais usado para conexão com uma fonte de dados é especificado nas propriedades da fonte de dados. Quando você abre um relatório do servidor de relatório, as credenciais de tempo de execução, especificadas nas propriedades da fonte de dados, talvez não funcionem para tarefas de tempo de design, como a criação de consultas e a visualização de relatórios. Por exemplo, a fonte de dados poderia usar credenciais do Windows diferentes das suas ou um nome de usuário e uma senha desconhecidos para você.  
  
 O Construtor de Relatórios abre a caixa de diálogo **Inserir Credenciais da Fonte de Dados** quando não pode se conectar à fonte de dados usando as credenciais fornecidas nas propriedades da fonte de dados. Geralmente isso ocorre quando:  
  
-   A fonte de dados é configurada para solicitar credenciais.  
  
-   A fonte de dados é configurada para usar credenciais armazenadas.  Para minimizar potenciais ameaças de segurança, o Construtor de Relatórios é criado para não recuperar credenciais armazenadas no servidor.  
  
 Você pode usar a caixa de diálogo **Inserir Credenciais da Fonte de Dados** para alterar as credenciais usadas pelo Construtor de Relatórios em tempo de design para se conectar à fonte de dados como o usuário atual do Windows ou fornecer um nome de usuário e uma senha. Se fornecer um nome de usuário e uma senha, você poderá indicar se eles são usados como credenciais do Windows.  
  
> [!NOTE]  
>  Embora os designers de consulta permitam a você especificar outro tipo de credenciais para credenciais em tempo de design, a visualização de relatório somente permite a inserção do nome do usuário e da senha para as opções de credenciais existentes especificadas na fonte de dados.  
  
 Quando você clicar em **Testar Conexão**, a conexão com a fonte de dados será testada com o uso das credenciais especificadas na página de credenciais de propriedades da fonte de dados. Você pode testar as conexões para fontes de dados inseridas e compartilhadas.  
  
 Se as credenciais especificadas estiverem incompletas (por exemplo, se uma senha for necessária), o Construtor de Relatórios solicitará novamente as credenciais de tempo de execução quando for necessário conectar à fonte de dados. As credenciais de tempo de design são armazenados e não serão solicitadas novamente.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da fonte de dados. O nome da fonte de dados deve ser exclusivo no relatório. Por padrão, um nome geral, como DataSource1 ou DataSource2, é atribuído à fonte de dados.  
  
 **Usar uma conexão compartilhada**  
 Selecione essa opção para localizar uma fonte de dados compartilhada que foi publicada no servidor de relatório.  
  
 Depois de selecionar uma fonte de dados em um servidor de relatório, o Construtor de Relatórios mantém uma conexão com esse servidor de relatório.  
  
 **Usar uma conexão inserida no meu relatório**  
 Selecione essa opção para criar uma nova fonte de dados que será usada somente por este relatório.  
  
 **Tipo**  
 Selecione uma extensão de processamento de dados. A lista exibe todas as extensões registradas.  
  
 **Cadeia de conexão**  
 Informe uma cadeia de conexão para a fonte de dados. Clique em **Construir** para criar a cadeia de conexão usando a caixa de diálogo **Propriedades da Conexão** . Clique no botão **Expressões** (*fx*) para editar a expressão.  
  
 **Usar uma única transação ao processar as consultas**  
 Selecione esta opção para indicar que os conjuntos de dados que usam essa fonte de dados serão executados em uma única transação no banco de dados. Para incluir as transações de sub-relatórios que usam a mesma fonte de dados, selecione o sub-relatório e, no painel Propriedades, defina **MergeTransactions** como **True**.  
  
 **Testar Conexão**  
 Clique para verificar se a conexão da fonte de dados funciona usando as credenciais especificadas. Se não for possível estabelecer a conexão, será necessário verificar suas credenciais e a disponibilidade do servidor. Você pode testar as conexões de fonte de dados para fontes de dados inseridas e compartilhadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Adicionar e verificar uma conexão de dados ou uma fonte de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Caixa de diálogo Propriedades da fonte de dados, credenciais &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md)   
 [Construtor de Relatórios ajuda para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)  
  
  
