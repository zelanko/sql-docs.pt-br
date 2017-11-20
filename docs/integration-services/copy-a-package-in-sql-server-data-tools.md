---
title: Copiar um pacote no SQL Server Data Tools | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 59a001e0aa360183e5e393faedc613cfabda0f02
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Copiar um pacote nas Ferramentas de Dados do SQL Server
  Este tópico descreve como criar um novo pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] por meio da cópia de um pacote existente e como atualizar as propriedades **Name** e **GUID** do novo pacote.  
  
### <a name="to-copy-a-package"></a>Para copiar um pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote que deseja copiar.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote.  
  
3.  Verifique se o pacote que será copiado está selecionado no Gerenciador de Soluções ou a guia no Designer SSIS que contém o pacote é a guia ativa  
  
4.  Sobre o **arquivo** menu, clique em **salvar \<nome do pacote > como**.  
  
    > [!NOTE]  
    >  O pacote deve ser aberto no Designer do SSIS antes que a opção **Salvar Como** aparecer no menu **Arquivo**.  
  
5.  Como opção, navegue até uma pasta diferente.  
  
6.  Atualize o nome do arquivo do pacote. Lembre-se de manter a extensão de arquivo .dtsx.  
  
7.  Clique em **Salvar**.  
  
8.  No prompt, escolha se deseja atualizar o nome do objeto de pacote para corresponder ao nome de arquivo. Se você clicar em **Sim**, a propriedade **Name** do pacote será atualizada. O novo pacote é adicionado ao projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e aberto no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
9. Como opção, clique no plano de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
10. Na janela Propriedades, clique no valor da propriedade de ID e, em seguida, na lista suspensa, clique em  **\<gerar nova ID >**.  
  
11. No menu **Arquivo** , clique em **Salvar Itens Selecionados** para salvar o novo pacote.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar uma cópia de um pacote](http://msdn.microsoft.com/library/21482a20-e420-4452-b7eb-8f9fa1929f31)   
 [Criar pacotes no SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40; SSIS &#41; Pacotes](../integration-services/integration-services-ssis-packages.md)  
  
  

