---
title: Alterando um assembly | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], modifying
- permissions [CLR integration]
- altering assemblies
- ALTER ASSEMBLY statement
ms.assetid: 9e765fbd-f339-473c-8537-22f478e79696
author: rothja
ms.author: jroth
ms.openlocfilehash: 80ef9d283f90c50406477a7a651fb418694ae445
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68027953"
---
# <a name="altering-an-assembly"></a>Alterando um assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os assemblies que foram registrados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem ser atualizados de uma versão mais recente que use a instrução ALTER ASSEMBLY. Para atualizar um assembly, use a instrução ALTER ASSEMBLY com a seguinte sintaxe:  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 A instrução ALTER ASSEMBLY não interrompe processos em execução que estejam usando o assembly; os processos continuam executando com o assembly inalterado. ALTER ASSEMBLY não pode ser usada para alterar as assinaturas de funções CLR (Common Language Runtime), funções de agregação, procedimentos armazenados e gatilhos. Novos métodos públicos podem ser adicionados ao assembly, métodos particulares podem ser modificados de alguma forma e métodos públicos podem ser modificados enquanto assinaturas ou atributos não são alterados. Os campos contidos em um tipo definido pelo usuário serializado nativo, incluindo membros de dados ou classes base, não podem ser alterados com o uso de ALTER ASSEMBLY. Não é oferecido suporte a todas as demais alterações. Para obter mais informações, consulte [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md).  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>Alterando o conjunto de permissões de um assembly  
 O conjunto de permissões de um assembly pode também ser alterado com a instrução ALTER ASSEMBLY. A instrução a seguir altera o conjunto de permissões do assembly SQLCLRTest para **EXTERNAL_ACCESS**.  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 Se o conjunto de permissões de um assembly estiver sendo alterado de **seguro** para **EXTERNAL_ACCESS** ou **não seguro**, uma chave assimétrica e o logon correspondente com permissão de **ASSEMBLY de acesso externo** ou permissão de **assembly insegura** para o assembly devem ser criados primeiro. Para obter mais informações, consulte [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md).  
  
## <a name="adding-the-source-code-of-an-assembly"></a>Adicionando o código-fonte de um assembly  
 A cláusula ADD FILE na sintaxe ALTER ASSEMBLY não está presente em CREATE ASSEMBLY. Você pode usá-la para adicionar código-fonte ou outros arquivos associados a um assembly. Os arquivos serão copiados dos seus locais originais e armazenados em tabelas do sistema do banco de dados. Isso garante que você sempre tenha código-fonte ou outros arquivos à mão, se precisar recriar ou documentar a versão atual do UDT.  
  
 A instrução a seguir adiciona o código-fonte de classe Point.cs para o UDT Point. O texto contendo o arquivo Point.cs será copiado e armazenado no banco de dados com o nome "PointSource".  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando assemblies de integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)   
 [Descartando um assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-assembly-transact-sql.md)  
  
  
