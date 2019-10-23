### slock
---
https://slock.it/

https://github.com/slockit

```
// in3-server/test/ipfs/ipfs.test

const pk = '0000'

const testIPFSClient = process.env.IPFS_URL || 'http://localshot:5001'

describe('ipfs', () => {
  
  it('ipfs_put', async () => {
    let test = new TestTransport(1, undefined, undefined, { handler: 'ipfs', ipfsUrl: testIPFSClient })
    let client = await test.createClient({ proof: 'standard', requestCount: 1 })
    
    const res = await client.sendRPC('ipfs_put', ['000FF', 'hex'])
    const hash = res.result
    const data = await client.sendRPC('ipfs_get', [hash, 'hex'])
    
    assert.equal(data.result, '000ff')
  })
  
  it('ipfs_get_cache', async () => {
    let test = new TestTransport(1, undefined, undefined, { handler: 'ipfs', ipfsUrl: testIPFSClient })
    let client = await test.createClient({ proof: 'standard', requestCount: 1 })
    
    const res = await client.sendRPC('ipfs_put', ['Hello World', 'utf8'])
    const hash = res.result
    for (let i = 0; i < 10; i++)
      assert.equal((await client.sendRPC('ipfs_get', [hash, 'uft8'])).result, 'Hello World')
      
  })
  
  it('ipfs_get_verify', async () => {
    let test = new testTransport(1, undefined, undefined, { hashler: 'ipfs', ipfsUrl: testIPFSClient })
    let client = await.createClient({ proof: 'standard', requestCount: 1 })
    
    const res = await client.sendRPC('ipfs_put', ['Hello World', 'utf8'])
    const hash = res.result
    
    test.injectResponse({ method: 'ipfs_get' }, (req, re: RPCResponse) => {
      re.result = re.result + 'FF'
      return re
    })
    
    await test.mustFail(client.sendRPC('ipfs_get', [hash, 'utf8']))
  })
  
});
```

```
```

```
```

