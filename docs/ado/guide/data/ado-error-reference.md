---
title: Referência de erro de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO], number reference
- errors [ADO], ErrorValueEnum
- ErrorValueEnum enumeration [ADO]
ms.assetid: f653393e-d4b0-4c34-ad5f-2bdf56bc1305
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5e1b20ffe6165688a438f97c2c23a7ac573ad320
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="ado-errors"></a>Erros de ADO
O **ErrorValueEnum** constante descreve os valores de erro de ADO. Para obter uma lista completa das constantes enumeradas, incluindo valores, consulte [apêndice b: ADO erros](../../../ado/guide/appendixes/appendix-b-ado-errors.md). Esta seção examinará alguns dos erros mais interessantes e explicar algumas situações específicas que podem gerá-los ou soluções para corrigir o problema. Ambos os **ErrorValueEnum** constante e o número de decimal positivo curto são listados.

|Número|Constante ErrorValueEnum|Descrição/possíveis causas|
|------------|-----------------------------|----------------------------------|
|**3000**|**adErrProviderFailed**|Falha do provedor ao executar a operação solicitada.|
|**3001**|**adErrInvalidArgument**|Argumentos são do tipo errado, estão fora do intervalo aceitável ou estão em conflito com uma da outra. Este erro geralmente é causado por um erro de digitação em uma instrução SQL SELECT. Por exemplo, um nome de campo incorreta ou o nome da tabela pode gerar esse erro. Esse erro também pode ocorrer quando um campo ou uma tabela chamada em uma instrução SELECT não existe no repositório de dados.|
|**3002**|**adErrOpeningFile**|Não foi possível abrir o arquivo. Foi especificado um nome de arquivo incorreta, ou um arquivo foi movido, renomeado ou excluído. Em uma rede, a unidade pode estar temporariamente indisponível ou o tráfego de rede pode estar impedindo a uma conexão.|
|**3003**|**adErrReadFile**|Não foi possível ler o arquivo. O nome do arquivo foi especificado incorretamente, o arquivo pode ter foi movido ou excluído ou o arquivo pode ter sido corrompido.|
|**3004**|**adErrWriteFile**|Gravar no arquivo falhou. Você pode ter fechado de um arquivo e, em seguida, tentou gravar nele, ou o arquivo pode estar corrompido. Se o arquivo está localizado em uma unidade de rede, condições de rede transitório podem impedir que a gravação em uma unidade de rede.|
|**3021**|**adErrNoCurrentRecord**|O **BOF** ou **EOF** for True, ou o registro atual foi excluído. A operação solicitada requer um registro atual.<br /><br /> Foi feita uma tentativa para atualizar registros usando **localizar** ou **busca** para mover o ponteiro do registro para o registro desejado. Se o registro não for encontrado, **EOF** será True. Esse erro também poderá ocorrer após uma falha **AddNew** ou **excluir** porque não há nenhum registro atual quando os métodos falharem.|
|**3219**|**adErrIllegalOperation**|Operação não é permitida neste contexto.|
|**3220**|**adErrCantChangeProvider**|O provedor fornecido é diferente do que já está em uso.|
|**3246**|**adErrInTransaction**|**Conexão** objeto não pode ser explicitamente fechado enquanto estiver em uma transação. Um **registros** ou **Conexão** objeto que atualmente está participando de uma transação não pode ser fechado. Chame **RollbackTrans** ou **CommitTrans** antes de fechar o objeto.|
|**3251**|**adErrFeatureNotAvailable**|O objeto ou o provedor não é capaz de executar a operação solicitada. Algumas operações dependem de uma versão específica do provedor.|
|**3265**|**adErrItemNotFound**|Item não foi encontrado na coleção correspondente para o nome solicitado ou ordinal. Um nome de tabela ou de campo incorreto foi especificado.|
|**3367**|**adErrObjectInCollection**|Objeto já está na coleção. Não é possível anexar. Um objeto não pode ser adicionado duas vezes na mesma coleção.|
|**3420**|**adErrObjectNotSet**|Objeto não é válido.|
|**3421**|**adErrDataConversion**|Aplicativo usa um valor do tipo errado para a operação atual. Você pode ter fornecido uma cadeia de caracteres para uma operação que aguarda um fluxo, por exemplo.|
|**3704**|**adErrObjectClosed**|Operação não é permitida quando o objeto está fechado. O **Conexão** ou **registros** foi fechado. Por exemplo, alguns outra rotina pode fechar um objeto global. Você pode evitar esse erro, verificando o **estado** propriedade antes de tentar uma operação.|
|**3705**|**adErrObjectOpen**|Operação não é permitida quando o objeto está aberto. Um objeto que está aberto não pode ser aberto. Campos não podem ser anexados a um aberto **registros**.|
|**3706**|**adErrProviderNotFound**|Provedor não pode ser encontrado. Ele talvez não esteja instalado corretamente.<br /><br /> O nome do provedor pode ser especificado incorretamente, o provedor especificado não pode ser instalado no computador onde o código está sendo executado, ou a instalação pode ter sido corrompida.|
|**3707**|**adErrBoundToCommand**|O **ActiveConnection** propriedade de um **registros** objeto, que tem um **comando** objeto como sua origem, não pode ser alterado. O aplicativo tentou atribuir um novo **Conexão** o objeto para um **registros** que tem um **comando** objeto como sua fonte.|
|**3708**|**adErrInvalidParamInfo**|**Parâmetro** objeto está definido incorretamente. Informações incompletas ou inconsistente foi fornecidas.|
|**3709**|**adErrInvalidConnection**|A conexão não pode ser usado para executar esta operação. Ele é fechado ou é inválido neste contexto.|
|**3710**|**adErrNotReentrant**|Operação não pode ser executada durante o processamento de eventos. Uma operação não pode ser executada dentro de um manipulador de eventos que faz com que o evento seja acionado novamente. Por exemplo, os métodos de navegação não devem ser chamados de dentro um **WillMove** manipulador de eventos.|
|**3711**|**adErrStillExecuting**|Não é possível executar a operação durante execução assíncrona.|
|**3712**|**adErrOperationCancelled**|Operação cancelada pelo usuário. O aplicativo tiver chamado o **CancelUpdate** ou **CancelBatch** método e a operação atual foi cancelada.|
|**3713**|**adErrStillConnecting**|Operação não pode ser executada durante a conexão de forma assíncrona.|
|**3714**|**adErrInvalidTransaction**|A transação de coordenação é inválida ou não foi iniciado.|
|**3715**|**adErrNotExecuting**|Operação não pode ser executada durante a execução não.|
|**3716**|**adErrUnsafeOperation**|As configurações de segurança deste computador proíbem acessar fonte de dados em outro domínio.|
|**3717**|**adWrnSecurityDialog**|Somente para uso interno. Não use. (Entrada foi incluída para manter a integridade. Esse erro não deve aparecer no seu código.)|
|**3718**|**adWrnSecurityDialogHeader**|Somente para uso interno. Não use. (Incluída para manter a integridade de entrada. Esse erro não deve aparecer no seu código.)|
|**3719**|**adErrIntegrityViolation**|O valor dos dados está em conflito com as restrições de integridade do campo. Um novo valor para um **campo** causaria uma chave duplicada. Um valor que compõe um lado de uma relação entre dois registros não pode ser atualizável.|
|**3720**|**adErrPermissionDenied**|Permissão insuficiente impede gravação no campo. O usuário chamado na cadeia de conexão não tem as permissões corretas para gravar um **campo**.|
|**3721**|**adErrDataOverflow**|Valor de dados é muito grande para ser representado pelo tipo de dados do campo. Um valor numérico que é muito grande para o campo desejado foi atribuído. Por exemplo, um valor inteiro longo foi atribuído a um campo de inteiro curto.|
|**3722**|**adErrSchemaViolation**|O valor dos dados está em conflito com o tipo de dados ou restrições do campo. O repositório de dados tem restrições de validação que difere do **campo** valor.|
|**3723**|**adErrSignMismatch**|Falha na conversão porque o valor dos dados tinha sinal e o tipo de dados de campo usado pelo provedor era sem sinal.|
|**3724**|**adErrCantConvertvalue**|Valor de dados não pode ser convertido por razões diferentes de sinais incompatíveis ou dados de estouro. Por exemplo, a conversão pode ter truncado dados.|
|**3725**|**adErrCantCreate**|Valor de dados não pode ser definido ou recuperado porque o tipo de dados de campo era desconhecido ou o provedor precisou recursos insuficientes para executar a operação.|
|**3726**|**adErrColumnNotOnThisRow**|Registro não contém este campo. Foi especificado um nome de campo incorreto ou um campo não o **campos** coleção do registro atual foi referenciada.|
|**3727**|**adErrURLDoesNotExist**|A URL de origem ou o pai da URL de destino não existe. Há um erro de digitação na URL de origem ou de destino. Você pode ter `http://mysite/photo/myphoto.jpg` quando você realmente deve ter `http://mysite/photos/myphoto.jpg` em vez disso. O erro de digitação na URL do pai (nesse caso, *foto* em vez de *fotos*) causou o erro.|
|**3728**|**adErrTreePermissionDenied**|As permissões são insuficientes para acessar a árvore ou subárvore. O usuário chamado na cadeia de conexão não tem as permissões apropriadas.|
|**3729**|**adErrInvalidURL**|URL contém caracteres inválidos. Verifique se que a URL foi digitada corretamente. A URL segue o esquema registrado para o provedor atual (por exemplo, o provedor de publicação é registrado para http).|
|**3730**|**adErrResourceLocked**|O objeto representado pelo URL especificado está bloqueado por um ou mais processos. Aguarde até que o processo foi concluído e tente a operação novamente. O objeto que você está tentando acessar foi bloqueado por outro usuário ou por outro processo no seu aplicativo. Isso é mais provável ocorrer em um ambiente multiusuário.|
|**3731**|**adErrResourceExists**|Operação de cópia não pode ser executada. Objeto nomeado pela URL de destino já existe. Especifique **adCopyOverwrite** para substituir o objeto. Se você não especificar **adCopyOverwrite** ao copiar os arquivos em um diretório, a cópia falhará ao tentar copiar um item que já existe no local de destino.|
|**3732**|**adErrCannotComplete**|O servidor não pode concluir a operação. Isso pode ser porque o servidor está ocupado com outras operações ou pode ser pouco recursos.|
|**3733**|**adErrVolumeNotFound**|Provedor não pode localizar o dispositivo de armazenamento indicado pela URL. Verifique se que a URL foi digitada corretamente. A URL do dispositivo de armazenamento pode estar incorretova, mas esse erro pode ocorrer por outros motivos. O dispositivo pode estar offline ou um grande volume de tráfego de rede pode impedir que a conexão de que está sendo feita.|
|**3734**|**adErrOutOfSpace**|Não é possível executar a operação. Provedor não é possível obter o espaço de armazenamento suficiente. Pode não haver suficiente RAM ou espaço em disco rígido para os arquivos temporários no servidor.|
|**3735**|**adErrResourceOutOfScope**|URL de origem ou destino está fora do escopo do registro atual.|
|**3736**|**adErrUnavailable**|Falha ao concluir operação e o status não está disponível. O campo pode estar indisponível ou a operação não foi tentada. Outro usuário pode ter alterado ou excluído o campo que você está tentando acessar.|
|**3737**|**adErrURLNamedRowDoesNotExist**|Registro nomeado pela URL não existe. Ao tentar abrir um arquivo usando um **registro** do objeto, o nome do arquivo ou o caminho para o arquivo foi digitado incorretamente.|
|**3738**|**adErrDelResOutOfScope**|A URL do objeto a ser excluído está fora do escopo do registro atual.|
|**3747**|**adErrCatalogNotSet**|Operação requer um válido **ParentCatalog**.|
|**3748**|**adErrCantChangeConnection**|Conexão foi negada. A nova conexão solicitada tem características diferentes das que já está em uso.|
|**3749**|**adErrFieldsUpdateFailed**|Falha na atualização de campos. Para obter mais informações, examine o **Status** propriedade dos objetos de campo individual. Esse erro pode ocorrer em duas situações: ao alterar uma **campo** o valor do objeto no processo de alteração ou adição de um registro para o banco de dados; e ao alterar as propriedades do **campo** objeto propriamente dito.<br /><br /> O **registro** ou **registros** Falha na atualização devido a um problema com um dos campos no registro atual. Enumerar o **campos** coleta e verifique se o **Status** propriedade de cada campo para determinar a causa do problema.|
|**3750**|**adErrDenyNotSupported**|Provedor não dá suporte a restrições de compartilhamento. Foi feita uma tentativa para restringir o compartilhamento de arquivo e o provedor não oferece suporte para o conceito.|
|**3751**|**adErrDenyTypeNotSupported**|Provedor não oferece suporte para o tipo solicitado de restrição de compartilhamento. Foi feita uma tentativa para estabelecer um tipo específico de compartilhamento de arquivos restrição que não é suportada pelo provedor. Consulte a documentação do provedor para determinar as restrições de compartilhamento de arquivos têm suporte.|
