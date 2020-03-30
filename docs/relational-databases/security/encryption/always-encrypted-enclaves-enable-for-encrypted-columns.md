---
title: Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: ad9346cacd3cb29b19245fb11b0d21c373d93738
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595651"
---
# <a name="enable-always-encrypted-with-secure-enclaves-for-existing-encrypted-columns"></a>Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes 
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

Este artigo descreve como desbloquear a funcionalidade do Always Encrypted com enclaves seguros e habilitar cálculos de enclave para as colunas criptografadas existentes.  

Se você tem colunas criptografadas com chaves que não são habilitadas para enclave, torne as colunas criptografadas com chaves habilitadas para enclave. Essa ação permitirá que você use o enclave seguro em consultas nas colunas.

Habilite os cálculos de enclave para as colunas criptografadas existentes de algumas maneiras diferentes, dependendo do seguinte:

- **Escopo/granularidade:** você deseja habilitar a funcionalidade de enclave para um subconjunto de colunas ou para todas as colunas protegidas por uma chave mestra de coluna especificada?
- **Tamanho dos dados:** qual é o tamanho das tabelas que contêm as colunas que você deseja habilitar para enclave?
- Você também deseja alterar o tipo de criptografia de suas colunas? Lembre-se de que somente a criptografia aleatória dá suporte a cálculos avançados (correspondência de padrões, operadores de comparação). Se a coluna for criptografada usando a criptografia determinística, você também precisará criptografá-la novamente com a criptografia aleatória para desbloquear cálculos avançados.

As seções a seguir descrevem as três abordagens usadas para habilitar enclaves nas colunas existentes.

## <a name="method-1-rotate-the-column-master-key-to-replace-it-with-an-enclave-enabled-column-master-key"></a>Método 1: Girar a chave mestra de coluna para substituí-la por uma chave mestra de coluna habilitada para enclave
A substituição de uma chave mestra de coluna existente (que não está habilitada para enclave) por uma nova chave mestra de coluna que está habilitada para enclave efetivamente torna todas as chaves de criptografia de coluna (associadas à chave mestra de coluna) também habilitadas para enclave.

- Prós:
  - não envolve criptografar novamente os dados, portanto, normalmente é a abordagem mais rápida. É uma abordagem recomendada para colunas que contêm grandes quantidades de dados, que já estão habilitadas para cálculos avançados e usam a criptografia determinística.
  - pode habilitar a funcionalidade de enclave para várias colunas em grande escala. A substituição da chave mestra de coluna pela chave mestra de coluna habilitada para enclave torna todas as chaves de criptografia de coluna e todas as colunas criptografadas associadas à chave mestra de coluna original habilitadas para enclave.
  
- Contras:
  - Não dá suporte à alteração do tipo de criptografia de determinística para aleatória. Embora desbloqueie a criptografia in-loco para colunas criptografadas usando a criptografia determinística, ele não habilita cálculos avançados. Você precisará criptografar novamente as colunas usando a criptografia aleatória.
  - Não permite que você converta seletivamente algumas das colunas associadas a uma chave mestra de coluna especificada.
  - Introduz uma sobrecarga de gerenciamento de chaves. Você precisará criar uma chave mestra de coluna e disponibilizá-la para os aplicativos que consultam as colunas afetadas.

Para obter informações sobre como girar uma chave mestra de coluna, confira [Girar chaves habilitadas para enclave](always-encrypted-enclaves-rotate-keys.md).

## <a name="method-2-rotate-the-column-master-key-and-re-encrypt-columns-using-randomized-encryption-in-place"></a>Método 2: Girar a chave mestra de coluna e criptografar novamente as colunas usando a criptografia aleatória in-loco
Esse método envolve a execução do Método 1 como a primeira etapa e, em seguida, a nova criptografia das colunas. As colunas começam usando a criptografia determinística e, em seguida, são criptografadas novamente com a criptografia aleatória para desbloquear consultas avançadas.

- Prós:
  - Criptografa novamente os dados in-loco. É um método recomendado se você precisa habilitar consultas avançadas para colunas criptografadas que atualmente usam a criptografia determinística e contêm grandes quantidades de dados. A etapa 1 (a rotação da chave mestra de coluna) desbloqueia a criptografia in-loco para colunas usando a criptografia determinística e a etapa 2 (nova criptografia das colunas) pode ser realizada in-loco.
  - pode habilitar a funcionalidade de enclave para várias colunas em grande escala.
  
- Contras:
  - Não permite que você converta seletivamente algumas das colunas associadas a uma chave mestra de coluna especificada.
  - Introduz uma sobrecarga de gerenciamento de chaves. Você precisará criar uma chave mestra de coluna e disponibilizá-la para os aplicativos que consultam as colunas afetadas.

Para obter informações sobre como girar uma chave mestra de coluna e criptografar novamente uma coluna in-loco para girar uma chave de criptografia de coluna, confira [Girar chaves habilitadas para enclave](always-encrypted-enclaves-rotate-keys.md).

## <a name="method-3-re-encrypt-a-selected-column-with-an-enclave-enabled-column-encryption-key-on-the-client-side"></a>Método 3: Criptografar novamente uma coluna selecionada com uma chave de criptografia de coluna habilitada para enclave no lado do cliente
Esse método envolve a nova criptografia de uma coluna com uma chave de criptografia de coluna habilitada para enclave e habilita consultas avançadas com a criptografia aleatória. Como a chave de criptografia de coluna atual não está habilitada para enclave, não é possível criptografar novamente a coluna in-loco. Use o assistente do Always Encrypted ou o cmdlet Set-SqlColumnEncryption para criptografar novamente a coluna fora do banco de dados.

- Prós:
  - Permite habilitar seletivamente a funcionalidade de enclave (criptografia in-loco e consultas avançadas, se você está criptografando novamente a coluna com a criptografia aleatória) para uma coluna ou um pequeno subconjunto de colunas.
  - Pode habilitar cálculos avançados para colunas em uma só etapa.
  - Não exige a criação de uma chave mestra de coluna e, portanto, tem um menor impacto sobre os aplicativos.
  
- Contras:
  - Para criptografar novamente os dados, a ferramenta os moverá para fora do banco de dados, o que pode levar muito tempo e está propenso a erros de rede.

Para obter mais informações sobre como girar uma criptografia de coluna por meio de uma ferramenta do lado do cliente, confira [Girar chaves do Always Encrypted usando o SQL Server Management Studio](rotate-always-encrypted-keys-using-ssms.md) e [Girar chaves do Always Encrypted usando o PowerShell](rotate-always-encrypted-keys-using-powershell.md).

## <a name="next-steps"></a>Próximas etapas
- [Consultar colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-query-columns.md)
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)
