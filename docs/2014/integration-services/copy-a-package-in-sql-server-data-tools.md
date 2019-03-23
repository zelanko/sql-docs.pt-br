---
title: Copiar um pacote no SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], copying
- copying packages
- regenerating package GUID
- updating package properties
ms.assetid: 03edc659-e76d-48c0-a749-5f1899b6b507
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 673b69ea632108b889cc2f99b63c9c602ef05237
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388805"
---
# <a name="copy-a-package-in-sql-server-data-tools"></a>Copiar um pacote nas Ferramentas de Dados do SQL Server
  Este descreve como criar um novo pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] por meio da cópia de um pacote existente e como atualizar as propriedades `Name` e `GUID` do novo pacote.  
  
### <a name="to-copy-a-package"></a>Para copiar um pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote que deseja copiar.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote.  
  
3.  Verifique se o pacote que será copiado está selecionado no Gerenciador de Soluções ou a guia no Designer SSIS que contém o pacote é a guia ativa  
  
4.  No menu **Arquivo**, clique em **Salvar \<nome do pacote> Como**.  
  
    > [!NOTE]  
    >  O pacote deve ser aberto no Designer do SSIS antes que a opção **Salvar Como** aparecer no menu **Arquivo** .  
  
5.  Como opção, navegue até uma pasta diferente.  
  
6.  Atualize o nome do arquivo do pacote. Lembre-se de manter a extensão de arquivo .dtsx.  
  
7.  Clique em **Salvar**.  
  
8.  No prompt, escolha se deseja atualizar o nome do objeto de pacote para corresponder ao nome de arquivo. Se você clicar **Yes**, o `Name` propriedade do pacote é atualizada. O novo pacote é adicionado ao projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e aberto no Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
9. Como opção, clique no plano de fundo da guia **Fluxo de Controle** e clique em **Propriedades**.  
  
10. Na janela Propriedades, clique no valor da propriedade de ID e, na lista suspensa, clique em **\<Gerar Nova ID>**.  
  
11. No menu **Arquivo** , clique em **Salvar Itens Selecionados** para salvar o novo pacote.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar uma cópia de um pacote](../../2014/integration-services/save-a-copy-of-a-package.md)   
 [Copiar pacotes nas Ferramentas de Dados do SQL Server](create-packages-in-sql-server-data-tools.md)   
 [Pacotes do SSIS &#40;Integration Services&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
