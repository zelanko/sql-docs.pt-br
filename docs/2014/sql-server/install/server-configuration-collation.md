---
title: Configuração do servidor-agrupamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- collation configuration, SQL Server
- collation configuration, Setup
- collation configuration
ms.assetid: e3986870-5be4-458b-b671-5ff12a27b022
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 521129056d4513af2f86fb7b70b26621cb881b80
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092286"
---
# <a name="server-configuration---collation"></a>Configuração do SQL Server – ordenação
  Na página Configuração do Servidor - Ordenação do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode modificar as configurações de ordenação usadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] e pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para fins de classificação. Selecione a opção para corresponder as configurações de ordenação de instalações diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de outro computador.  
  
## <a name="options"></a>Opções  
 Personalizar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece dois grupos de ordenações: ordenações do Windows e ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode especificar configurações de ordenação separadas para o [!INCLUDE[ssDE](../../includes/ssde-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou especificar a mesma ordenação para ambos.  
  
 Por padrão, uma ordenação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é selecionada para localidades do sistema do idioma inglês. A ordenação padrão para versões localizadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é determinada pela configuração de localidade do sistema Windows em seu computador.  
  
 As configurações padrão devem ser alteradas apenas se a configuração de ordenação dessa instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corresponder às configurações de ordenação usadas por outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou se ela corresponder à localidade do sistema Windows de outro computador.  
  
 **Observação** [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa somente agrupamentos do Windows. Se você planeja instalar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], selecione uma ordenação do Windows durante o processo de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para garantir a consistência dos resultados entre o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para obter mais informações, veja [Configurações de ordenação na Instalação](https://go.microsoft.com/fwlink/?LinkId=190977).  
  
## <a name="best-practices"></a>Práticas Recomendadas  
 Para obter mais informações sobre uma tabela de localidades de Sistema do Windows e as ordenações padrão correspondentes usadas pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Configurações de ordenação na Instalação](https://go.microsoft.com/fwlink/?LinkId=190977).  
  
 Se possível, use uma ordenação exclusiva para sua organização. Dessa forma, não será preciso especificar explicitamente a ordenação para cada banco de dados, coluna, expressão ou identificador. Se você precisar trabalhar com várias ordenações e configurações de página de códigos diferentes, codifique suas consultas para considerar as regras da precedência de ordenação. Para obter mais informações, confira o tópico [Precedência de ordenação &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql) nos Manuais Online.  
  
 Quando você selecionar uma ordenação para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere as seguintes recomendações:  
  
-   Selecione uma ordenação BINARY2 se ordenação binária baseada em ponto de código for aceitável.  
  
-   Selecione uma ordenação do Windows para que a comparação seja consistente em todos os tipos de dados.  
  
-   Use uma nova ordenação nível 100 para obter um suporte melhor à classificação lingüística. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md).  
  
-   Caso você pretenda migrar um banco de dados para a instância atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione a ordenação correspondente à sua ordenação existente do banco de dados.  
  
  
