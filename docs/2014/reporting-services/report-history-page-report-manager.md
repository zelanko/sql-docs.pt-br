---
title: Relatar a página de histórico (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4c64e58a-ed83-4e29-a422-9baaac2be4b8
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cb6d9de69656d40b3a5fd87c5353c6d0b8f0ef5f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56033857"
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
  
3.  No menu suspenso, clique em **Exibir Histórico de Relatórios**.  
  
## <a name="options"></a>Opções  
 **Delete (excluir)**  
 Clique para excluir um ou mais instantâneos. Antes de clicar em **Excluir**, marque a caixa de seleção ao lado do instantâneo que você deseja excluir.  
  
 **Novo instantâneo**  
 Clique para adicionar um instantâneo a um histórico de relatório. Esse botão é disponibilizado quando você escolhe a opção **Permitir que o histórico seja criado manualmente** na página de propriedades do Histórico do relatório.  
  
 **Última Execução**  
 Exibe a data e a hora em que o instantâneo foi criado. Clique em uma descrição para exibir um instantâneo específico.  
  
 **Tamanho**  
 Exibe o tamanho da definição do relatório mais os dados no relatório. Esse valor indica quanto espaço no banco de dados do servidor de relatórios é usado pela definição e dados do relatório. O tamanho do relatório renderizado, que inclui formatação, é maior, na verdade. O tamanho total, indicado entre parênteses, é igual à soma de todos os instantâneos no histórico de relatório para o relatório atual.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir ou excluir histórico de relatório &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/view-or-delete-report-history-report-manager.md)   
 [Adicionar um instantâneo ao histórico de relatório &#40;Gerenciador de Relatórios&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Página Propriedades Gerais, Relatórios &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Página de propriedades Opções de instantâneo &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/snapshot-options-properties-page-report-manager.md)  
  
  
