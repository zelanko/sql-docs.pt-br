---
title: Página Histórico de relatórios (Report Manager) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 0b0841e031ee1a98f4f678406f790996a709e90f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104475"
---
# <a name="report-history-page-report-manager"></a>Página Histórico de Relatório (Gerenciador de Relatórios)

Use a página Histórico de Relatório para exibir instantâneos de relatório que são gerados e armazenados ao longo do tempo. Dependendo das opções definidas no servidor de relatório, o histórico do relatórios poderá conter somente os instantâneos mais recentes.  
  

O histórico de relatório é sempre exibido no contexto do relatório de origem. Você não pode exibir o histórico de todos os relatórios em um servidor de relatórios em um único lugar.  
  
Para gerar histórico de relatórios, o relatório deve ser executado de modo autônomo (ou seja, ele deve usar credenciais armazenadas; relatórios com parâmetros devem conter valores de parâmetro padrão para todos os parâmetros). Histórico de Relatórios pode ser gerado manualmente ou como uma operação agendada. As propriedades de histórico no relatório determinam os modos pelos quais o histórico do relatório pode ser criado.  
  
Você pode clicar em um instantâneo de histórico de relatórios para exibi-lo. Instantâneos exibidos em histórico de relatórios só são diferenciados pela data e hora em que foram criados. Não existe indicação visual para distinguir se um relatório foi gerado em resposta a uma operação programada ou manual.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-report-history-page"></a>Para abrir a página Histórico de Relatórios  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cujos instantâneos você deseja exibir.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Exibir Histórico de Relatório**.  
  
## <a name="options"></a>Opções  
 **Delete (excluir)**  
 Clique para excluir um ou mais instantâneos. Antes de clicar em **Excluir**, marque a caixa de seleção ao lado do instantâneo que você deseja excluir.  
  
 **Novo Instantâneo**  
 Clique para adicionar um instantâneo a um histórico de relatório. Esse botão é disponibilizado quando você escolhe a opção **Permitir que o histórico seja criado manualmente** na página de propriedades do Histórico do relatório.  
  
 **Última Execução**  
 Exibe a data e a hora em que o instantâneo foi criado. Clique em uma descrição para exibir um instantâneo específico.  
  
 **Tamanho**  
 Exibe o tamanho da definição do relatório mais os dados no relatório. Esse valor indica quanto espaço no banco de dados do servidor de relatórios é usado pela definição e dados do relatório. O tamanho do relatório renderizado, que inclui formatação, é maior, na verdade. O tamanho total, indicado entre parênteses, é igual à soma de todos os instantâneos no histórico de relatório para o relatório atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir ou excluir o histórico de relatórios &#40;Report Manager&#41;](../../2014/reporting-services/view-or-delete-report-history-report-manager.md)   
 [Adicionar um instantâneo ao histórico de relatório &#40;Report Manager&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Página Propriedades gerais, relatórios &#40;Report Manager&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Ajuda F1 Report Manager](../../2014/reporting-services/report-manager-f1-help.md)   
 [Página Propriedades de opções de instantâneo &#40;Report Manager&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)