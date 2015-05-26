#include <iostream>
#include <algorithm>
#include <string>
#include <vector>

using namespace std;

typedef vector<vector<char> > vec2char;

vec2char str2board(string s);

/*
   first List of Letters:
   	all letters in the board
   2nd List of Letters:
   	adjacent(meetFirstLetter( 1st List of Letters))
   3rd List of Letters:
   	adjacent(meetSecondLetter(2nd List of Letters))
 */

class Road {
public:
	// constractor
	Road(pair<int, int> size) 
	{
		// init
		for(auto ix = pm.begin(); ix != pm.end(); ix++) 
		{
			for(auto iy = ix->begin(); iy != ix->end(); iy++)
			{
				*iy = 0;
			}
		}
	}

	void moveTo(pair<int, int> p)
	{
		path.push_back(p);
		pm.at(p.first).at(p.second) = 1;
	}

	pair<int, int> getCur()
	{
		return path.back();
	}

	bool inPath(pair<int, int> p)
	{
		int x = p.first;
		int y = p.second;
		if(pm.at(x).at(y) == 1) 
		{
			return true;
		}
		else
		{
			return false;
		}
	}

private:

	vector<pair<int, int>> path;

	// path matrix
	vector<vector<int>> pm;

};

class Board : public vec2char 
{

public:
	// constractor
	Board(string s) {

		vec2char ix = str2board(s);

		// assign
		this->assign(ix.begin(), ix.end());

		// get size
		initSize();

		// init letterPosList
		initPosition();
	}

	Board(vec2char board) {

		vec2char* ix = this;

		// copy
		ix->assign(board.begin(), board.end());

		// get size
		initSize();

		initPosition();

	}


	// loop until length of letterPosList == 0
	bool exist(string word) {

		// letter list not empty

		auto is = word.begin();

		while(is != word.end()) {

			meetLetter(*is);

			// no next candidate
			if(letterPosList.size() == 0) {
			
				break;
			}

			is++;
		}

		// return 
		if(is == word.end()) {
			return true;
		}
		else {
			return false;
		}

	}

	// print
	void printBoard() {
		// loop through the Board
		for(	auto ix = this->begin() ; ix != this->end() ; ix++ ) {
			for (	auto iy = ix->begin() ; iy != ix->end() ; iy++ ) {
				cout << *iy << " ";
			}
			cout << "\n";
		}

	}

	// print pair
	void printPair() {

		for(auto iter = letterPosList.begin() ; iter != letterPosList.end() ; iter++) {
			cout 	<< "<"
				<< iter->first
			     	<< ","
			     	<< iter->second
				<< ">"
				<< endl;
		}
	}
	
	// print other pair
	void printOrtherPair(vector< pair<int, int> > vp) {

		for(auto iter = vp.begin() ; iter != vp.end() ; iter++) {
			cout 	<< "<"
				<< iter->first
			     	<< ","
			     	<< iter->second
				<< ">"
				<< endl;
		}
	}

	// at
	using vec2char::at;
	//@override
	char at(int i, int j) {
		vec2char* x = this;
		return x->at(i).at(j);
	}

	//@override
	char at(pair<int, int> p) {
		vec2char* x = this;
		int i = p.first;
		int j = p.second;
		return x->at(i).at(j);
	}

	// test find char in a Board
	void testA(char A) {
		// 1. init a Board check
		//  . print Board
		// 2. meet letter return vp
		// 3. print list of pos

		// 1
		printBoard();
		// 2
		vector< pair<int, int> > vp = listMeetLetter(A);
		// 3
		printOrtherPair(vp);

	}
	
	// test right of an element 
	void testRight(int i, int j) {

		pair<int, int> p = make_pair(i, j);

		pair<int, int> r = right(p);

		pair<int, int> s = size;
		
		cout	<< "Size: "
			<< s.first << ", "
			<< s.second
			<< endl;

		cout 	<< "This Point: "
			<< i << ", "
			<< j << endl;

		cout 	<< "right: " 
			<< r.first << ", "
			<< r.second
			<< endl;
			


	}


private:

	// String to board
	vec2char str2board(string s) {

		vec2char ix;
		vector<char> iy;
		// push back string
		for( 	string::iterator is = s.begin() ; is != s.end() ; is++ ) {

			// skip "space"
			if (*is == ' ') {
				continue;
			}

			// start new line when meet ';'
			if (*is == ';') {
				ix.push_back(iy);
				iy.clear();
			}
			// normal char
			else {
				iy.push_back(*is);
			}
		}
		return ix;
	}

	// List of position of Letters
	vector<Road> letterPosList; 

	// size of the Board
	pair<int, int> size;

	// Update After Meet A Letter
	void meetLetter(char c) {

		// update Position List after meet a letter;
		letterPosList = neighbourList(listMeetLetter(c));
	}

	// Neighbor List of a vector of road
	vector<Road> neighbourList(vector<Road> vr) {

		vector<Road> vrResult;
		for(auto iter = vr.begin(); iter != vr.end(); iter++) {

			// TODO:
			// examine point in the path
			// if in the path, then not add to the list
			// if not in the path, add to the list
			vector<Road> vrNeighbour = neighbour(*iter);
			// insert neighbour vector
			vrResult.insert(vrResult.end(), vrNeighbour.begin(), vrNeighbour.end());
		}

		return vrResult;
	}

	// List Meet Letter
	vector< pair<int, int> > listMeetLetter(char c) {

		vector< pair<int, int> > vp;

		for(auto iter = letterPosList.begin(); iter != letterPosList.end(); iter++) {

			// if value at position == c then push_back curr position
			if(this->at(*iter) == c) {

				vp.push_back(*iter);
			}
		}

		return vp;
		
	}

	// Borad to List of Positions
	void initPosition() {
		int i = 0;
		int j = 0;
		pair<int, int> p;

		// Init Positions
		for(auto ix = this->begin() ; ix != this->end() ; ix++) {
			for(auto iy = ix->begin() ; iy != ix->end() ; iy ++) {

				p = make_pair(i, j);
				letterPosList.push_back(p);
				j++;
			}
			j = 0;
			i++;
		}
	}

	// Size of the Board

	// Neighbour of The Point
	// TODO:
	// change neighbour of a point to neighbour of a Road
	vector<Road> neighbour(Road r) 
	{
		vector<Road> vr;

		Road tmpR = r;

		pair<int, int> p = r.getCur();

		if(left(p) != p && !r.inPath(left(p))) {
			// TODO:
			// push_back?
			tmpR.moveTo(left(p));
			vr.push_back(tmpR);
			tmpR = r;
		}

		if(up(p) != p && !r.inPath(up(p))) {
			tmpR.moveTo(up(p));
			vr.push_back(tmpR);
			tmpR = r;
		}

		if(right(p) != p && !r.inPath(right(p))) {
			tmpR.moveTo(right(p));
			vr.push_back(tmpR);
			tmpR = r;
		}

		if(down(p) != p && !r.inPath(down(p))) {
			tmpR.moveTo(down(p));
			vr.push_back(tmpR);
			tmpR = r;
		}

		return vr;
	}

	// Move Around The Point
		// Left of the Point
	pair<int, int> left(pair<int, int> p) {

		if(p.second > 0) {

			return make_pair(p.first, p.second - 1);
		}
		else {

			return p;
		}
	}

		// Up of the Point
	pair<int, int> up(pair<int, int> p) {

		if(p.first > 0) {

			return make_pair(p.first - 1, p.second);
		}
		else {

			return p;
		}
	}

		// Right of the Point
	pair<int, int> right(pair<int, int> p) {

		pair<int, int> s = this->size;
		if(p.second < s.second - 1) {

			return make_pair(p.first, p.second + 1);
		}
		else {

			return p;
		}
	}

		// Down of the Point
	pair<int, int> down(pair<int, int> p) {

		pair<int, int> s = this->size;
		if(p.first < s.first - 1) {

			return make_pair(p.first + 1, p.second);
		}
		else {

			return p;
		}
	}

	void initSize() {
		vec2char* vc = this;
		int lx = vc->size();
		int ly = vc->at(0).size();

		this->size = make_pair(lx, ly);
	}
};

class Solution {
public:

	bool exist(vector<vector<char>>& board, string word) 
	{

		Board b(board);
		bool hasWord = b.exist(word);

		if(hasWord)
		{
			return true;
		}
		else
		{
			return false;
		}

	}

};

int main(int argc, char** argv) {

	string s = 
		  "A B C D A" 
		"; E A G H G" 
		"; I J A L K" 
		"; M N L A P;";
	/*
	string s = 
		"a a a a"
		"; a a a a"
		"; a a a a;";
		*/
	vec2char v = str2board(s);
	string word = "ABABABABABA";
	Solution sol;
	bool hasWord = sol.exist(v, word);

	cout << hasWord << endl;

	//b.testRight(1, 4);

	return 0;
}


// String to board
vec2char str2board(string s) 
{

	vec2char ix;
	vector<char> iy;
	// push back string
	for( 	string::iterator is = s.begin() ; is != s.end() ; is++ ) {

		// skip "space"
		if (*is == ' ') {
			continue;
		}

		// start new line when meet ';'
		if (*is == ';') {
			ix.push_back(iy);
			iy.clear();
		}
		// normal char
		else {
			iy.push_back(*is);
		}
	}
	return ix;
}
