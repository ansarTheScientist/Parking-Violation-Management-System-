#include"XDD.h"
//Custom Header File


#include <iostream>
#include <string>
#include <fstream>
#include <sstream>
#include <vector>
#include <math.h> // floor()
#include <iostream>
#include <bits/stdc++.h>

using namespace std;


//class ParkingRecord;

class ParkingRecord {
public:
	
    string colums[50];
    ParkingRecord() {}
    ParkingRecord(string cols[50]){
		for(int i = 0 ; i < 43 ; i++){
        	colums[i] = cols[i]; 
		}

    }

    void display(const vector<ParkingRecord>& parking ) {
        for(int i = 0 ; i < 43 ; i++){
        	cout<<parking [0].colums[i]<<" : "<<colums[i]<<endl; 
		}
			
		cout<<endl;
    	//parking [i]
	}
};

struct Node
{
    long int key;      
    string val[50] ;
    Node *next;   

    Node() : key(0),  next(0){};
    Node(long int Key, string *s  ) :  key(Key), next(0){
				
		for(int i = 0 ;  i < 50 ; i ++){
			val[i] = s[i] ;
		}	
	}

 //   Node(Node const &data) : key(data.key), value(data.value), next(data.next){
//	
//		for(int i = 0 ;  i < 50 ; i ++){
//			val[i] = data.val[i] ;
//		}			
	
//	}


};

class HashTable
{
private:
public:
	string sss ;
	long int max ;
	long int *count_n ;
    Node **table; 
    void tableDoubling();
    void reHashing(int size_orig);

    int size,     
        count;    
    HashTable(){};
    HashTable(int m) : size(m), count(0) , max(0) 
    {
    	count_n = new long int[size]{} ;
        table = new Node *[size]; 
        for (int i = 0; i < size; i++)
            table[i] = 0; 
    }
    ~HashTable();

    int hashFunction(int key);
    void Insert(long int key , string *s , int num);  
    void Search(string s);
    void displayTable();
    void displaysearch(int i,string s);

};


void Search(HashTable *ht, string s){

	int len = sizeof(s);
	int asci = 0;
	for(int i = 0 ; i < len && s[i] != 0 ; i++ ){
			if(s[i] < 'd'){
				asci = asci * 10 ;
			}else {
				asci = asci * 100 ;
			}
			asci = asci + int(s[i]) ;
			
		}
//			cout << asci << endl ;
	
	int key = ht->hashFunction(asci);
	
	ht->displaysearch(key,s);		
	
	
}




void HashTable::Insert(long int key  , string *s , int col)
{
    count++;
    if (count > size)
    {                    
        tableDoubling(); 
    }

    int index = hashFunction(key); 
    Node *newNode = new Node(key  , s);     

    // push_front()
    if (table[index] == NULL)
    {                           
        table[index] = newNode; 
    }
    else
    {                                    
        Node *next = table[index]->next; 
        table[index]->next = newNode;
        newNode->next = next;
    }
  count_n[index] ++ ;
  if(max < count_n[index] ){
  max = count_n[index] ;
  sss = table[index]->val[col] ;
  }

 // cout << count_n[index] << " at index  " << s[33] << endl ;
}


void test(HashTable *tr){
	
	cout << "Most common value is : "<<tr->sss << endl;
	cout << "With the amount of "<<tr->max <<" occurences."<< endl ;
	
}



int HashTable::hashFunction(int key)
{
   
    double A = 0.6180339887, frac = key * A - floor(key * A);
    return floor(this->size * frac);
}

void HashTable::tableDoubling()
{
    int size_orig = size; 
    size *= 2;            
    reHashing(size_orig); 
}

void HashTable::reHashing(int size_orig)
{
	long int *newcount = new long int [size] ; 
    Node **newtable = new Node *[size]; 	
   
	for (int i = 0; i < size; i++)
    {                   
    	newcount[i] = 0 ;
	    newtable[i] = 0;
    }

    for (int i = 0; i < size_orig; i++)
    {

        Node *curr_orig = table[i], 
            *prev_orig = NULL;      
		
        while (curr_orig != NULL)
        { 
			 prev_orig = curr_orig->next; 
            int index = hashFunction(curr_orig->key); 

            if (newtable[index] == NULL)
            { 
                newtable[index] = curr_orig;
                newtable[index]->next = 0; 
            }
            else
            {                                       
                Node *next = newtable[index]->next; 
                newtable[index]->next = curr_orig;
                curr_orig->next = next;
            }
            curr_orig = prev_orig; 
        	newcount[index] ++ ;
		}
    }
    delete [] count_n ;
    this->count_n = newcount ;
    delete[] table;         
    this->table = newtable; 
}

HashTable::~HashTable()
{
    for (int i = 0; i < size; i++)
    {                             
        Node *current = table[i]; 
        while (current != NULL)
        { 
            Node *previous = current;
            current = current->next;
            delete previous;
            previous = 0;
        }
    }
    delete[] table;
}

void HashTable::displayTable()
{
    for (int i = 0; i < size; i++)
    { // visit every node in table
        Node *current = table[i];
        while (current != NULL)
        {
            for(int j = 0 ; j < 50 ; j++){
            	cout << current->val[j] << "    "  ;
			}
			cout <<endl <<endl;
            current = current->next;
        }
        cout << endl;
    }
    cout << endl;
}

void HashTable::displaysearch(int i,string s){
	int count = 0;
	Node *current = table[i];
        while (current != NULL)
        {
            for(int j = 0 ; j < 50 ; j++){
            	cout << current->val[j] << "    "  ;
			}
			cout <<endl<<endl<<endl ;
			count++;
            current = current->next;
        }
        cout << endl;
	
	cout<<endl<<endl;
	
	
	cout<<"The Total Number of "<<s<<" is : "<<count<<endl<<endl;	
}



struct node
{	string id ;
	string id2[50] ; 
	ParkingRecord *data ;
	struct node *left;
	struct node *right;
}*root;

class BST{
	private :
		node *root ;
	public :
		BST(){
			root = 0;
		}
		int height(node *temp)
		{
			int h = 0;
			if (temp != NULL)
			{
				int l_height = height(temp->left);
				int r_height = height(temp->right);
				int max_height = max(l_height, r_height);
				h = max_height + 1;
			}
			return h;
		}
		int diff(node *temp)
		{
			int l_height = height(temp->left);
			int r_height = height(temp->right);
			int b_factor = l_height - r_height;
			return b_factor;
		}
		node *rr_rotation(node *parent)
		{
			node *temp;
			temp = parent->right;
			parent->right = temp->left;
			temp->left = parent;
			return temp;
		}
		node *ll_rotation(node *parent)
		{
			node *temp;
			temp = parent->left;
			parent->left = temp->right;
			temp->right = parent;
			return temp;
		}
		node *lr_rotation(node *parent)
		{
			node *temp;
			temp = parent->left;
			parent->left = rr_rotation(temp);
			return ll_rotation(parent);
		}
		node *rl_rotation(node *parent)
		{
			node *temp;
			temp = parent->right;
			parent->right = ll_rotation(temp);
			return rr_rotation(parent);
		}	
		
		node *balance(node *temp)
		{
			int bal_factor = diff(temp);
			if (bal_factor > 1)
			{
				if (diff(temp->left) > 0)
					temp = ll_rotation(temp);
				else
					temp = lr_rotation(temp);
			}
			else if (bal_factor < -1)
			{
				if (diff(temp->right) > 0)
					temp = rl_rotation(temp);
				else
					temp = rr_rotation(temp);
			}
			return temp;
		}
		
		node *insert(node *root , ParkingRecord *data  ,string s1 , string *s){
			if (root == NULL)
			{
				root = new node;
				root->id = s1;
				for(int i = 0 ; i < 50 ; i++ ){
					root->id2[i] = s[i] ;
				}
				root->data = data ;
				root->left = NULL;
				root->right = NULL;
				return root;
			}
			else if (s1 < root->id)
			{
				root->left = insert(root->left, data , s1 , s);
				root = balance(root);
			}
			else if (s1 >= root->id)
			{
				root->right = insert(root->right, data , s1 , s);
				root = balance(root);
			}
			return root;
		}
		
		void inorder(node *tree , int disp )
		{	
			if (tree == NULL)
				return;
			inorder(tree->left, disp);
			for(int i = 0 ; i < disp ; i++ ){
			cout <<  tree->id2[i]  ;
			if(tree != root){
				cout << "		" ;
			}
			}
			cout << endl ;
			inorder(tree->right , disp );
		}		
					
};


void insertg(vector<ParkingRecord>& parking , long long int disp2  )
{
	long long int j=0;
	string s ;
	BST d ;
    for (auto cardata : parking ) {
    	if(j!=0){
    		
    	s = cardata.colums[1] ;
    	root = d.insert(root , &cardata , s , cardata.colums) ;
		   //	cardata.display(parking ); 
       			
		}
        j++;
        if(j>disp2){
        	break;
		}
    }
	
}

void inset_t(vector<ParkingRecord>& parking ,HashTable *ht , int col ,long long int disp2){

	string s ;
	long long int j = 0 ;
	for(auto cardata : parking ){
	long int asci = 0 ;
		if(j != 0){
		int len = sizeof(cardata.colums[col]) ;
		s = cardata.colums[col] ;
	//	cout << s << endl ;
		for(int i = 0 ; i < len && s[i] != 0 ; i++ ){
			if(s[i] < 'd'){
				asci = asci * 10 ;
			}else {
				asci = asci * 100 ;
			}
			asci = asci + int(s[i]) ;
			
//			cout << asci << endl ;
		}
		
		ht->Insert(asci , cardata.colums ,col );
		}
		j++ ;
		if(j > disp2){
			break ;
		}
	}
	//	ht->displayTable() ;
	
}  
void displayparking (int disp ) {
	BST d ;
    d.inorder(root , disp) ;
}




int main()
{
	intro();
	mid();
    ifstream inputFile;
    inputFile.open("Parking_Violations_Issued_-_Fiscal_Year_2017.csv");
    string line = "" , opt ;
	int k = 0 ;
    vector<ParkingRecord> parking ;
    while (getline(inputFile, line) && k<500000) {
		string colums[50] ;
		int i=0;
        stringstream inputString(line);
        
		//cardataId, Last Name, FirstName, Age, Phone Number, GPA
//        string cardataId;
//        string lastName;
//        string firstName;
//  
		for(i=0;i<43;i++){
        	getline(inputString, colums[i], ',');
		}
        //getline(inputString, lastName, ',');
        //getline(inputString, firstName, ',');
  		
        ParkingRecord cardata(colums);
        parking .push_back(cardata);
        line = "";
        k++;
    }
	int n = 0 ;
	do{
	HashTable *ht = new HashTable (12) ;
	system("cls") ;
	cout << "-------------Menu------------" << endl ;
	cout << "List of options " << endl ;
	cout << "	1. Display all data " << endl ;
	cout << "	2. Detail analysis " << endl ;
	cout << "	3. exit " << endl ;
	
	
	

			long long int disp2 ;
	cin >> n ;
	switch(n){
		case 1 :
			int disp   ;
			cout << "Enter the number of parameters you want to display " << endl ;
    		cin >> disp ;
    		cout << "Enter the number of entries you want to display " << endl ;
    		cin >> disp2	;
			insertg(parking,disp2);
			displayparking (disp);
				cout << "press any to continue " << endl ;
	cin >> opt ;
			break ;
		case 2 :
			int col_num ;
			system("CLS");
			cout<<"PARAMETR OPTIONS"<<endl;
			cout<<"1. Plate ID\t\t2. Registration State\t\t3. Plate Type\t\t4.Issue date\t\t5.Violation Code\t\t6.Violation Body"<<endl<<endl;
			cout<<"7.Vehicle Make\t\t8.Issuing Agency\t\t9.Street Code 1\t\t10.Street Code 2\t\t11.Street Code 3\t\t12.Vehicle Expiration Date"<<endl<<endl;
			cout<<"13.Violatio Location\t\t14.Violation Precint\t\t15.Issuer Precint\t\t16.Issuer Code\t\t17.Issuer Command \t\t18.Issuer Squad"<<endl<<endl;
			cout<<"19. Violation Time\t\t20. Time First Observed\t\t21. Violation County\t\t22. Violation In Front Of Or Opposite\t\t23. House number\t\t24. Street Name"<<endl<<endl;
			cout<<"25. Intersecting Street\t\t26. Date First Observed\t\t27. Law Section\t\t28. Sub Diision\t\t29. Violation Legal Code\t\t30. Days Parking In Effect"<<endl<<endl;
			cout<<"31. From Hours In Effect\t\t32. TO Hours In Effect\t\t33. Vehicle Color\t\t34. Unregistered Vehicle?\t\t35. Vehicle Year\t\t36. Meter Number"<<endl<<endl;
			cout<<"37. Feet From Curb\t\t38. Violation Post Code\t\t39. Violation Description\t\t40.No Standing or Stopping Violation\t\t41. Hydrant Violation\t\t42. Double Parking Violation"<<endl<<endl;
			
			{
			string s;
			cout<<"Do you want to?"<<endl;
			cout<<"1. Sort the file by Any Parameters?"<<endl;
			cout<<"2. Search a Specific Constant Value in a Parameter?"<<endl;
			cout<<"3. Find most occurrences of a Constant Value in a Parameter?"<<endl;
			int hhh = 0;
			cin>>hhh;
			
			if(hhh==1){
				cout << "Enter the parameter from where you want to sort " ;
				cin >> col_num ;
				cout << "Enter the number of entries to display : " << endl ; 
				cin >> disp2 ;
				inset_t(parking , ht , col_num , disp2 ) ;
				ht->displayTable();
			}
			else if(hhh==2){
				cout << "Enter the parameter from where you want to search from : " ;
				cin >> col_num ;
				cout << "Enter the number of entries to analyse : " << endl ; 
				cin >> disp2 ;
				cout<<"Enter Constant you want to search : ";
				fflush(stdin);
				getline(cin,s);
				inset_t(parking , ht , col_num , disp2 ) ;
				Search(ht,s);
				
			}
			else if(hhh==3){
				cout<<"Enter the parameter you want to analyse from : ";
				cin >> col_num ;
				cout << "Enter the number of entries to analyse : " << endl ; 
				cin >> disp2 ;
				inset_t(parking , ht , col_num , disp2 ) ;
				test(ht);

					
			}

			}
				cout << "press any to continue " << endl ;
			cin >> opt ;
			break ;
		case 3 :
			end();
			break ;
			
		default :
			cout << "Invalid input " << endl  ;
			cout<< "press any key to continue " ;
			string abc;
			cin >>  abc;
			continue ;
			break ;			
	}

	delete ht;
	}while (n != 3 ) ;


	//end();


	return 0 ;


}
