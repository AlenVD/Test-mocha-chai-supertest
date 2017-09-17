# Test-mocha-chai-supertest

const app = require('../app');

const supertest = require('supertest');
const chai = require('chai');
const expect = chai.expect;
const should = chai.should;

//var assert= require('chai').assert;

const api = supertest('http://localhost:3000');

let login = null;
let users = null;
describe('Tests', () => {

	// Login user to the system and fetch access token
	it('Login user', (done) => {
		api.post('/sign-in')
			.send({
				password: 'password',
				email: 'email',
			})
			.then((res) => {
				login = res.body.access_token;
				done();
			}).
			catch(done);
	});

	// Get a list of all users
	it('Get users list', (done) => {
		api.get('/users')
			.set('authorization', login)
			.then((res) => {
				// we expect that there is 6 users. You can check/confirm that in app code.
				expect(res.body.length).to.be.equal(6);
				done();
			}).
		catch(done);
	});

	//returns hello world
	it('returns hello world', function(done) {
		api.get('/')
		.expect('Hello World!', done);
	});
	

	// Checking array
	it('Array', (done) => {
		api.get('/users')
			.set('authorization', login)
			.then((res) => {
				expect(res.body).to.be.a('array');
				expect(res.body).to.not.be.empty;
				done();
			}).
		catch(done);
	});

	//Be sure there is less then 7 users
	it('Less than 7', (done) => {
		api.get('/users')
			.set('authorization', login)
			.then((res) => {
				expect(res.body.length).to.be.lessThan(7);
				done();
			}).
		catch(done);
	});

	//Be sure there is more then 5 users
	it('More then 5', (done) => {
		api.get('/users')
			.set('authorization', login)
			.then((res) => {
				expect(res.body.length).to.be.above(5);
				done();
			}).
		catch(done);
	});

	// Cheking token
	it('Token', (done) => {
		api.post('/sign-in')
			.send({
				password: 'password',
				email: 'email',
			})
			.then((res) => {
				expect(res.body.access_token).to.equal('00000000-0000-0000-0000-000000000000');
				done();
			}).
			catch(done);
	});

		

		// Checking error Res
		it('Error responses', (done) => {
			api.get('/users/:4')
			.set('authorization', login)	
				.then((res) => {
					expect(res.body).to.has.property('error');
					expect(res.body).to.has.property('message');
					expect(res.body).to.has.property('stack');
					done();
				}).
			catch(done);
		});
	
       
		

		//expect(res.text).to.be.equal('sss');

		

        


});

// I am trying to test datas
it("Testing datas", function() {
	var MyObectj1 = {
		user_id: 1,
		name: 'User The One',
		title: 'Pljeskavica master',
		active: true,
	};
	var MyObectj2 = {
		user_id: 2,
		name: 'User The Two',
		title: 'Rakija master',
		active: true,
	};
	var MyObectj3 = {
		user_id: 3,
		name: 'User The Three',
		title: 'Salata master',
		active: false,
	};
	var MyObectj4 = {
		user_id: 4,
		name: 'User The Four',
		title: 'Drugstore master',
		active: false,
	};
	var MyObectj5 = {
		user_id: 5,
		name: 'The Master',
		title: 'Evil timelord',
		active: true,
	};
	var MyObectj6 = {
		user_id: 6,
		name: 'The Doctor',
		title: 'Good timelord',
		active: true,
	};
	
	 
	expect(MyObectj1.active).to.be.equal(MyObectj2.active);
	expect(MyObectj1).to.not.be.equal(MyObectj2);
	expect(MyObectj5.name).to.not.be.equal(MyObectj6.name);
	expect(MyObectj3.user_id).to.be.greaterThan(MyObectj2.user_id);

	expect(MyObectj1.user_id).to.be.a('number');
	expect(MyObectj2.user_id).to.be.a('number');
	expect(MyObectj3.user_id).to.be.a('number');
	expect(MyObectj4.user_id).to.be.a('number');
	expect(MyObectj5.user_id).to.be.a('number');
	expect(MyObectj6.user_id).to.be.a('number');
	expect(MyObectj1.name).to.be.a('string');
	expect(MyObectj2.name).to.be.a('string');
	expect(MyObectj3.name).to.be.a('string');
	expect(MyObectj4.name).to.be.a('string');
	expect(MyObectj5.name).to.be.a('string');
	expect(MyObectj6.name).to.be.a('string');
    expect(MyObectj1.active).to.be.a('boolean');
	expect(MyObectj2.active).to.be.a('boolean');
	expect(MyObectj3.active).to.be.a('boolean');
	expect(MyObectj4.active).to.be.a('boolean');
	expect(MyObectj5.active).to.be.a('boolean');
	expect(MyObectj6.active).to.be.a('boolean');
	
	});
