//C++ Program to implement Trie data structure

#include <iostream.h>

using namespace std;
 

#define CHAR_SIZE 128
 

class Trie
{
public:
    bool isLeaf;
    Trie* Chara[CHAR_SIZE];
 
    
    Trie()
    {
        this->isLeaf = false;
 
        for (int j = 0; j < CHAR_SIZE; j++) {
            this->Chara[j] = nullptr;
        }
    }
 
    void insert(string);
    bool deletion(Trie*&, string);
    bool search(string);
    bool haveChildren(Trie const*);
};
 

void Trie::insert(string key)
{
    
    Trie* curr = this;
    for (int j = 0; j < key.length(); j++)
    {
        
        if (curr->Chara[key[j]] == nullptr) {
            curr->Chara[key[j]] = new Trie();
        }
 
        
        curr = curr->Chara[key[j]];
    }
 
    
    curr->isLeaf = true;
}
 

bool Trie::search(string key)
{
    
    if (this == nullptr) {
        return false;
    }
 
    Trie* curr = this;
    for (int j = 0; j < key.length(); j++)
    {
        
        curr = curr->Chara[key[j]];
 
    
        if (curr == nullptr) {
            return false;
        }
    }
    
    return curr->isLeaf;
}
 

bool Trie::haveChildren(Trie const* curr)
{
    for (int j = 0; j < CHAR_SIZE; j++)
    {
        if (curr->Chara[j]) {
            return true;    
        }
    }
 
    return false;
}
 
bool Trie::deletion(Trie*& curr, string key)
{
    
    if (curr == nullptr) {
        return false;
    }
 
    
    if (key.length())
    {
        
 
        if (curr != nullptr &&
            curr->Chara[key[0]] != nullptr &&
            deletion(curr->Chara[key[0]], key.substr(1)) &&
            curr->isLeaf == false)
        {
            if (!haveChildren(curr))
            {
                delete curr;
                curr = nullptr;
                return true;
            }
            else {
                return false;
            }
        }
    }
 
    
    if (key.length() == 0 && curr->isLeaf)
    {
        
        if (!haveChildren(curr))
        {
        
            delete curr;
            curr = nullptr;
 
            
            return true;
        }
 
        
        else {
            
            curr->isLeaf = false;
 

            return false;
        }
    }
 
    return false;
}
 

int main()
{
    Trie* head = new Trie();
 
    head->insert("hello");
    cout << head->search("hello") << " ";      
 
    head->insert("helloworld");
    cout << head->search("helloworld") << " "; 
 
    cout << head->search("helll") << " ";      
 
    head->insert("hell");
    cout << head->search("hell") << " ";       
 
    head->insert("h");
    cout << head->search("h");            
 
    cout << endl;
 
    head->deletion(head, "hello");
    cout << head->search("hello") << " ";     
 
    cout << head->search("helloworld") << " "; 
    cout << head->search("hell");              
 
    cout << endl;
 
    head->deletion(head, "h");
    cout << head->search("h") << " ";          
    cout << head->search("hell") << " ";       
    cout << head->search("helloworld");       
 
    cout << endl;
 
    head->deletion(head, "helloworld");
    cout << head->search("helloworld") << " ";
    cout << head->search("hell") << " ";       
 
    head->deletion(head, "hell");
    cout << head->search("hell");              
 
    cout << endl;
 
    if (head == nullptr) {
        cout << "Trie empty!!\n";              
    }
 
    cout << head->search("hell");             
 
    return 0;
}




