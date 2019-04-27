---
title: Restaurar do PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql11.asvs.ssmsimbi.RestoreFromPP.f1
ms.assetid: 232ac8ed-77fe-47d8-acd3-59bc2fdfdf48
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 21b3c477c87861d224d72a52dcce89ceacf7bb3a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756569"
---
# <a name="restore-from-powerpivot"></a>Restaurar do PowerPivot
  Você pode usar o recurso Restaurar do PowerPivot no SQL Server Management Studio para criar um novo banco de dados modelo de tabela em uma instância do Analysis Services (executando em modo Tabular) ou restaurar para um banco de dados existente de uma pasta de trabalho PowerPivot (.xlsx).  
  
> [!NOTE]  
>  O modelo de projeto Importar do PowerPivot no SQL Server Data Tools fornece funcionalidade semelhante. Para obter mais informações, consulte [importar do PowerPivot &#40;SSAS de tabela&#41;](import-from-power-pivot-ssas-tabular.md).  
  
 Ao usar Restaurar do PowerPivot, tenha em mente o seguinte:  
  
-   Para usar o recurso Restaurar do PowerPivot, você deverá estar conectado como membro da função Administradores de Servidor na instância do Analysis Services.  
  
-   A conta de serviço da instância do Analysis Services deve ter permissões de leitura no arquivo da pasta de trabalho que você está restaurando.  
  
-   Por padrão, quando você restaura um banco de dados do PowerPivot, a propriedade Informações de Representação da Fonte de Dados do banco de dados modelo de tabela é definida como padrão, que especifica a conta de serviço da instância do Analysis Services. É recomendável alterar as credenciais de representação para uma conta de usuário do Windows em Propriedades do Banco de Dados. Para obter mais informações, consulte [Representação &#40;SSAS de Tabela&#41;](impersonation-ssas-tabular.md).  
  
-   Os dados no modelo de dados PowerPivot serão copiados para um banco de dados modelo de tabela novo ou existente na instância do Analysis Services. Se sua pasta de trabalho PowerPivot contiver tabelas vinculadas, elas serão recriadas como uma tabela sem uma fonte de dados, semelhante a uma tabela criada usando Colar em nova tabela.  
  
### <a name="to-restore-from-powerpivot"></a>Para restaurar do PowerPivot  
  
1.  No SSMS, na instância do Active Directory para a qual você deseja restaurar, clique com o botão direito em **Bancos de dados**e clique em **Restaurar do PowerPivot**.  
  
2.  Na caixa de diálogo **Restaurar do PowerPivot** , em **Restaurar Origem**, em **Arquivo de backup**, clique em **Procurar**e selecione um arquivo .abf ou .xslx do qual restaurar.  
  
3.  Em **Destino da Restauração**, em **Restaurar banco de dados**, digite um nome de um banco de dados novo ou existente. Se você não especificar um nome, o nome da pasta de trabalho será usado.  
  
4.  Em **Local de armazenamento**, clique em **Procurar**e selecione um local para armazenar o banco de dados.  
  
5.  Em **Opções**, deixe **Incluir informações de segurança** marcado. Ao restaurar de uma pasta de trabalho PowerPivot, essa configuração não se aplica.  
  
## <a name="see-also"></a>Consulte também  
 [Bancos de dados de modelo de tabela &#40;SSAS de Tabela&#41;](tabular-model-databases-ssas-tabular.md)   
 [Importar do PowerPivot &#40;Tabular do SSAS&#41;](import-from-power-pivot-ssas-tabular.md)  
  
  
